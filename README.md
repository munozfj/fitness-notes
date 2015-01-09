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
git remote add origin git@github.com:munozfj/project.git
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










```sh

```  