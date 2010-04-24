--- 
layout: post
title: Overriding Resource Controller Defaults
---
h2. The problem

I was having a lot of repetition while I was overriding some ResourceController defaults. I don't like to be redirect to the show action after the create/update operation, and I also needed the flash messages in spanish (as you can see in the code). 

The following code shows how I solved it, but in no case is the only solution. This is only the one that removes a lot of repetition in my code. 

I was looking for some sort of hint about how to do this on the RC list, but I didn't find it. 

h2. The solution

So, here's te code: 

<filter:code lang="ruby">module ResourceController
  class Driven < ActionController::Base
    unloadable
    
    def self.inherited(subclass)
      super
      subclass.class_eval do 
        resource_controller
      subclass.class_eval do 
        resource_controller
        create.before { object.creador = current_usuario if object.respond_to?(:creador) }
        
        create.wants.html { redirect_to_return_path_or collection_path }
        create.flash { "#{object.class.to_s.underscore.humanize} ha sido agregado con éxito. Puedes accederlo haciendo click #{@template.link_to('aquí', object_path)}."}
        create.failure.flash { "Ought!"}
        
        update.wants.html { redirect_to_return_path_or collection_path }
        update.flash { "#{object.class.to_s.underscore.humanize} ha sido modificado con éxito. Puedes accederlo haciendo click #{@template.link_to('aquí', object_path)}."}
        update.failure.flash { "Ought!"}
        
        destroy.flash { "#{object.class.to_s.underscore.humanize} ha sido eliminado con éxito!"}
      end
    end
  end
end
</filter:code>

The only way I found to do all this was to implement a different class to inherit from. So I end up doing also this at the RAILS_ROOT/app/controllers/application.rb.

<filter:code lang="ruby">
class ApplicationController < ResourceController::Driven
...
# code...
...
end
</filter:code>

NOTE: I am inheriting from my own implementation of RC, not from ResourceController::Base.

h2. Conclusion

You can also thrown a lot more. In my current project I am exposing the resources/models as json and xml. 
One way to avoid repetition is to include all the "action.wants.format" (show.wants.json, index.wants.xml, etc) in this custom implementation, like this:


<filter:code lang="ruby">module ResourceController
  class Driven < ActionController::Base
    unloadable
    
    def self.inherited(subclass)
      super
      subclass.class_eval do
        # before this there should be an invocation to resource_controller, 
        # and probably the code from the first example.  
        index.wants.xml  { render :xml  => collection}
        index.wants.json { render :json => collection}
        #... an so on...
      end
    end
  end
end
</filter:code>

Hope you enjoy.
