# Fitness Notes

Autor:            Fernando J. Muñoz 

Descripción:      El objetivo de esta aplicación es poder registrar el progreso en un plan 
                  de fitness y de dieta. 

Fecha de inicio:  09/01/2015

---
## Fecha: 09/01/2015

###Objetivo:
- Crear una aplicacion
- Subirla en Github
- Subirla en Heroku

###Pasos:
- cd Sites
- ruby -v
- rails -v
- Crear la aplicación
```sh
rails _4.2.0_ new fitness-notes
```  
- cd fitness-notes
- mv README.rdoc README.md
- Modificar Gemfile
```sh
source 'https://rubygems.org'

ruby '2.2.0'
gem 'rails', '4.2.0'

gem 'sass-rails', '~> 5.0'
gem 'uglifier', '>= 1.3.0'
gem 'coffee-rails', '~> 4.1.0'

gem 'jquery-rails'
gem 'turbolinks'
gem 'jbuilder', '~> 2.0'

gem 'rails-html-sanitizer', '~> 1.0.1'
gem 'bootstrap-sass', '~> 3.3.0.1'
gem 'will_paginate', '~> 3.0.7'
gem 'will_paginate-bootstrap', '~> 1.0.1'

group :development do
  gem 'annotate', '~> 2.6.5'
  gem 'better_errors', '~> 2.1.0'
  gem 'binding_of_caller', '~> 0.7.2'
  gem 'quiet_assets', '~> 1.1.0'
  gem 'rails_layout', '~> 1.0.24'
end

group :development, :test do
  gem 'sqlite3', '~> 1.3.10'
  gem 'byebug', '~> 3.5.1'
  gem 'web-console', '~> 2.0.0'
  gem 'spring', '~> 1.2.0'
end

group :production do
  gem 'pg', '~> 0.18.1' 
  gem 'rails_12factor', '~> 0.0.3'
end

gem 'sdoc', '~> 0.4.1', group: :doc
```  
- Instalar las gemas con
```sh
bundle install --without production 
```  
- Instalar annotate con:
```sh
rails g annotate:install
```  
- Para guardar también las rutas hacer
```sh
annotate --routes
``` 
- Ir a GitHub y crear ahi el repositorio fitness-notes
- Comenzamos a registrar los cambios con GIT
```sh
git init
git add -A
git commit -m "Commit inicial"
``` 
- Subimos las modificaciones a GitHub
```sh
git remote add origin git@github.com:munozfj/fitness-notes.git
git push -u origin master
``` 
- Publicar en Heroku
```sh
RAILS_ENV=production rake assets:precompile
heroku create fitness-notes
git push heroku master
heroku config:set SECRET_KEY_BASE=`ruby -rsecurerandom -e "puts SecureRandom.hex(64)"`
heroku apps:rename project
heroku logs
heroku open
``` 
---
##Fecha: 09/01/2015
###Objetivos:
- Crear páginas estáticas
- Establecer Root
- Crear rutas con nombre

###Pasos:
- Creo una nueva rama de desarrollo y me cambio a la pagina
```sh
git co -b pag-estaticas 
```
- Crear las paginas estaticas
```sh
rails g controller Static home contact about help forum --no-assets  --no-helper
```
- Modificar el archivo /config/routes.rb para que tenga pagina root
```sh
root 'static#home' 
```
- Crear nombres para las paginas estaticas
```sh
get 'contact', to: 'static#contact', as: 'contact'
get 'about', to: 'static#about', as: 'about'
get 'help', to: 'static#help', as: 'help'
get 'forum', to: 'static#forum', as: 'form'
```
- Reiniciar el servidor web para que tome los cambios realizados
- Registrar en routes.rb las nuevas rutas
```sh
annotate --routes
```
- Para ver los nombres de las rutas hacer
```sh
rake routes
```
- Modificar levemente las vistas de las paginas estáticas
- Confirmar cambios en la rama
```sh
git branch
git status
git add -A
git commit -m "Paginas estaticas"
```
- Coloco los cambios de la rama en MASTER
```sh
git co master
git branch
git merge <nombre rama aux>
```
- Subir los cambios a GitHub
```sh
git push
```
- Subir los cambios a Heroku
```sh
RAILS_ENV=production rake assets:precompile
git push heroku
heroku open  
```
- La rama auxiliar se podria eliminar
```sh
git branch
git -d <nombre rama aux>
```










```sh

```  