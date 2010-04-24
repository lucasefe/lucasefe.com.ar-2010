--- 
layout: post
title: "Extendi\xE9ndonos con Ruby/Rails"
---
Hoy me agarré la cabeza mal. 

Estaba haciendo  un plugin para engancharle un comportamiento al plugin acts_as_state_machine (AASM) y me mandé una genial. 
El código en cuestión era el siguiente. Si nos fijamos entre la línea 18 a la 20 extiendo el comportamiento de AASM. Todo parece muy lindo. 

<filter:code lang="ruby">module Driven
  module Monitoreable
    def self.included(base)
      base.extend Driven::Monitoreable::Base
    end
    module Base
      def acts_as_state_machine_monitoreable(o = {})
        options = { :reraise => true }.merge(o)
        
        include InstanceMethods
        
        class_inheritable_accessor :reraise
        write_inheritable_attribute :reraise, options[:reraise]
        
        class_eval do
          has_many :monitor_mensajes, 
                          :class_name => 'Monitor::Mensaje', 
                          :as => :monitoreable
          extend ClassMethods
          ScottBarron::Acts::StateMachine::InstanceMethods.class_eval do 
            include Driven::AasmExtension::InstanceMethods
          end
          ScottBarron::Acts::StateMachine::SupportingClasses::StateTransition.class_eval do
           include Driven::AasmExtension::StateTransition 
          end
          ScottBarron::Acts::StateMachine::SupportingClasses::Event.class_eval do
            include Driven::AasmExtension::Event
          end
        end
      end
    end
  end
 ......
</filter:code>

Los módulos/métodos que le  incluyo son los siguientes:

<filter:code lang="ruby">module AasmExtension
    module StateTransition
      def self.included(base)
        base.alias_method_chain :perform, :monitoring
      end
      def perform_with_monitoring(record)
        record.log "Evolucionando de '#{@from}' a '#{@to}'"
        perform_without_monitoring(record)
      end
    end
    module Event
      def self.included(base)
        base.alias_method_chain :fire, :monitoring
      end
      def fire_with_monitoring(record)
        record.log "Evento: #{@name}"
        fire_without_monitoring(record)
      end
    end
    module InstanceMethods
      def self.included(base)
        base.alias_method_chain :run_transition_action, :monitoring
      end
      def run_transition_action_with_monitoring(action)
        monitor do
          run_transition_action_without_monitoring(action)
        end
      end
    end
  end
end
</filter:code>

*Noten que estoy usando alias_method_chain...*

Para hacerla corta, cuando usaba este mixin en un solo modelo de rails, funcionaba todo bien, pero en cuanto eran 2 o más los que lo implementaban, comenzaba a recibir Stack Level Too Deep extensions por todos lados. 

Tardé un rato, pero me di cuenta. Estaba incluyendo Driven::AasmExtension más de una vez en AASM, entonces terminaba llamandose una y otra vez a si mismo, y nunca llegaba a ejecutar la acción real. Recursividad que no se resuelve. Muy despistado...

Cómo lo solucioné?

Asegurandome que no se incluya más de una vez a Driven::AasmExtension. 

<filter:code lang="ruby">def acts_as_state_machine_monitoreable(o = {})
        options = { :reraise => true }.merge(o)
        
        include InstanceMethods
        
        class_inheritable_accessor :reraise
        write_inheritable_attribute :reraise, options[:reraise]
        
        class_eval do
          has_many :monitor_mensajes, :class_name => 'Monitor::Mensaje', :as => :monitoreable
          extend ClassMethods
          unless ScottBarron::Acts::StateMachine::InstanceMethods.included_modules.include?(Driven::AasmExtension::InstanceMethods)
          ScottBarron::Acts::StateMachine::InstanceMethods.class_eval do 
            include Driven::AasmExtension::InstanceMethods
          end
          ScottBarron::Acts::StateMachine::SupportingClasses::StateTransition.class_eval do
           include Driven::AasmExtension::StateTransition 
          end
          ScottBarron::Acts::StateMachine::SupportingClasses::Event.class_eval do
            include Driven::AasmExtension::Event
          end
          end
        end
      end
</filter:code>

Bueh, que la experiencia me sirva, y ojalá que no le pase nadie, porque me volví loco para darme cuenta.
