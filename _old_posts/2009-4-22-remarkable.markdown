--- 
layout: post
title: Remarkable
---
Rspec es genial. Out-of-the-box te provee unos "meta-matchers" bastante piolas. Si tenés un método que retorne un boolean y termine en ? podés preguntar algo como esto:

<filter:code lang="ruby">describe User do
  # suponiendo que @user responde a admin?
  subject { User.new }
  it { should be_admin } 
end</filter:code>

Súper copado, pero nada nuevo. Claro, cuando te empezás a meter un poco más, descubrís que muchas de los matchers que usás siempre, alguien ya las "metió" en un módulo y las puso disponibles para todos. Dos ejemplos de ello son "rspec_on_rails_matchers":http://github.com/joshknowles/rspec-on-rails-matchers/tree/master (buen inicio, pero se quedó en el tiempo) y "shoulda":http://thoughtbot.com/projects/shoulda/ (que es excelente).

La cuestión es que después de usar shoulda una semana, di con "Remarkable":http://remarkable.rubyforge.org/ (luego de escuchar, creo, a los pibes de "RailsEnvy":http://www.railsenvy.com .

Remarkable es una gema que incluye espectations y matchers para usar dentro y fuera de rails. La lista es interminable, pero voy a hacer un mini-raconto de lo que estuve usando esta semana (con un supuesto modelo User):

<filter:code lang="ruby">describe User
  subject { Factory.build(:user) }
  it { should validate_presence_of(:first_name) }
  it { should validate_presence_of(:last_name) }
  it { should have_many(:posts) }
end

describe Post
  subject { Factory.build(:post) }
  # Db matchers
  it { should have_columns(:title, :body, :permalink)}
  it { should have_index([:title]).unique(true) 
  
  # Validaciones Active Record
  it { should validate_presence_of(:title) }
  it { should validate_uniqueness_of(:title, :scope => 'topic') }
  it { should validate_uniqueness_of :title, :allow_blank => true} 
 
  # Relaciones 
  # se verificará que el counter cache se incluya como opción y 
  # que el campo esté definido en la DB. 
  # No hay una en que no me olvide de esto. 
  it { should belong_to(:topic, :counter_cache => true) }
  it { should belong_to(:user, :counter_cache => true) } 
  # se verificará que se incluya el :through como opción 
  # además de que exista la relación.
  it { should have_many(:comments) }
  it { should have_many(:viewers, :through => :comments) }

  # named scopes
  it { should have_scope(:published).conditions(:published => true) }

  # acepta colecciones cómo parámetros
  it { should allow_mass_assignment_of(:title, :body, :tags, :permalink) }
end
</filter:code>

Además de esto, podemos integrarlo con I18n y generar los specs en castellano, u otro idioma. Funciona exactamente igual que Rails, ya que usa la misma gema (svenfuchs-i18n). O sea, nuestro cliente no tiene que saber inglés para entender nuestros specs. Esto, por lo menos para mi, es oro puro. 

Como si esto fuera poco, además provee un forma de crear matchers muy fácilmente (un mini DSL), "sin reinventar la rueda":http://remarkable.rubyforge.org/core/.

En el ejemplo yo solo hablé de la parte de Active Record, pero también incluye un montón de matchers para el ActionController y próximamente para ActionView también ("Acá":http://remarkable.rubyforge.org/rails/).

h2. Instalación

  sudo gem install remarkable_rails

En Rails 2.3, para que Remarkable se cargue correctamente hay que incluir lo siguiente en config/environments/test.rb

  config.gem "rspec",            :lib => false
  config.gem "rspec-rails",      :lib => false
  config.gem "remarkable_rails", :lib => false

Y después requerir remarkable dentro de spec_helper.rb, justo después de "spec/rails":

  require 'spec/rails'
  require 'remarkable_rails'

Para mi resultó muy útil, y no veo razón alguna para no usarlo de aquí en más (más allá de incluir una nueva dependencia).

Si tienen la libertad de poder incluir/sugerir mejoras en sus proyectos actuales, y se cansaron de escribir siempre lo mismo, entonces prueben Remarkable. Posta, te hace la vida mucho más simple. Ojo, hay que pensar igual :P
