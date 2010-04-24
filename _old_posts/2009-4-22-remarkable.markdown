--- 
layout: post
title: Remarkable
---
Rspec es genial. Out-of-the-box te provee unos "meta-matchers" bastante piolas. Si ten�s un m�todo que retorne un boolean y termine en ? pod�s preguntar algo como esto:

<filter:code lang="ruby">describe User do
  # suponiendo que @user responde a admin?
  subject { User.new }
  it { should be_admin } 
end</filter:code>

S�per copado, pero nada nuevo. Claro, cuando te empez�s a meter un poco m�s, descubr�s que muchas de los matchers que us�s siempre, alguien ya las "meti�" en un m�dulo y las puso disponibles para todos. Dos ejemplos de ello son "rspec_on_rails_matchers":http://github.com/joshknowles/rspec-on-rails-matchers/tree/master (buen inicio, pero se qued� en el tiempo) y "shoulda":http://thoughtbot.com/projects/shoulda/ (que es excelente).

La cuesti�n es que despu�s de usar shoulda una semana, di con "Remarkable":http://remarkable.rubyforge.org/ (luego de escuchar, creo, a los pibes de "RailsEnvy":http://www.railsenvy.com .

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
  # se verificar� que el counter cache se incluya como opci�n y 
  # que el campo est� definido en la DB. 
  # No hay una en que no me olvide de esto. 
  it { should belong_to(:topic, :counter_cache => true) }
  it { should belong_to(:user, :counter_cache => true) } 
  # se verificar� que se incluya el :through como opci�n 
  # adem�s de que exista la relaci�n.
  it { should have_many(:comments) }
  it { should have_many(:viewers, :through => :comments) }

  # named scopes
  it { should have_scope(:published).conditions(:published => true) }

  # acepta colecciones c�mo par�metros
  it { should allow_mass_assignment_of(:title, :body, :tags, :permalink) }
end
</filter:code>

Adem�s de esto, podemos integrarlo con I18n y generar los specs en castellano, u otro idioma. Funciona exactamente igual que Rails, ya que usa la misma gema (svenfuchs-i18n). O sea, nuestro cliente no tiene que saber ingl�s para entender nuestros specs. Esto, por lo menos para mi, es oro puro. 

Como si esto fuera poco, adem�s provee un forma de crear matchers muy f�cilmente (un mini DSL), "sin reinventar la rueda":http://remarkable.rubyforge.org/core/.

En el ejemplo yo solo habl� de la parte de Active Record, pero tambi�n incluye un mont�n de matchers para el ActionController y pr�ximamente para ActionView tambi�n ("Ac�":http://remarkable.rubyforge.org/rails/).

h2. Instalaci�n

  sudo gem install remarkable_rails

En Rails 2.3, para que Remarkable se cargue correctamente hay que incluir lo siguiente en config/environments/test.rb

  config.gem "rspec",            :lib => false
  config.gem "rspec-rails",      :lib => false
  config.gem "remarkable_rails", :lib => false

Y despu�s requerir remarkable dentro de spec_helper.rb, justo despu�s de "spec/rails":

  require 'spec/rails'
  require 'remarkable_rails'

Para mi result� muy �til, y no veo raz�n alguna para no usarlo de aqu� en m�s (m�s all� de incluir una nueva dependencia).

Si tienen la libertad de poder incluir/sugerir mejoras en sus proyectos actuales, y se cansaron de escribir siempre lo mismo, entonces prueben Remarkable. Posta, te hace la vida mucho m�s simple. Ojo, hay que pensar igual :P
