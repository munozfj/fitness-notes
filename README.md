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
---
##Fecha: 09/01/2015
###Objetivos:
- Mdificar el layout de la aplicacion con rails_layout
- Utilizar Bootstrap

###Pasos:
- Creo una nueva rama de desarrollo
```sh
git co -b layout
```
- Para modificar el layout de la aplicación para que use Bootstrap3
```sh
rails generate layout:install bootstrap3 --force 
```
- Como se va a utilizar autenticacion por devise, genero el navigation para eso
```sh
rails generate layout:navigation --force 
```
- Modificar el archivo _navigation_links.html.erb
```sh
<%# add navigation links to this file %>
<li><%= link_to 'Home', root_path %></li>
<li><%= link_to 'About', about_path %></li>
<li><%= link_to 'Contact', contact_path %></li>
<li><%= link_to 'Forum', forum_path %></li>
```
- Crear /views/layouts el partial footer
```sh
<!-- Footer -->
<hr>
<footer>
<small>FM &copy; Company <%= Time.now.year %></small>
</footer>
```
- Crear /views/layouts el partial _favicon.html.erb
```sh
<!-- https://www.iconfinder.com -->
<!-- https://www.iconfinder.com/icons/85827/scale_weight_icon#size=30 -->
<!-- Favicon tradicional -->
<%= favicon_link_tag 'app.png', rel: 'shortcut icon' , type: 'image/png'%>
<!-- Favincon para Appel y Android -->
<%= favicon_link_tag 'app-60.png', rel: 'apple-touch-icon', type: 'image/png' , size:'60x60' %>
<%= favicon_link_tag 'app-72.png', rel: 'apple-touch-icon', type: 'image/png' , size:'72x72' %>
<%= favicon_link_tag 'app-120.png', rel: 'apple-touch-icon', type: 'image/png' , size:'120x120' %>
<%= favicon_link_tag 'app-152.png', rel: 'apple-touch-icon', type: 'image/png' , size:'152x152' %>
<%= favicon_link_tag 'app.png', rel: 'apple-touch-icon-precomposed', type: 'image/png' %>
```
- Colocar en la carpeta /assets/images las imagenes que funcionaran como iconos de la aplicacione
- Crear /views/layouts el partial _metas.html.erb
```sh
<meta charset="utf-8">
<meta http-equiv="X-UA-Compatible" content="IE=edge">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="description" content="Fitness Notes">
<meta name="author" content="Fernando J. Muñoz">
```
- Crear /views/layouts el partial _shim.html.erb
```sh
<!-- HTML5 shim and Respond.js IE8 support of HTML5 elements and media queries -->
<!--[if lt IE 9]>
<script src="https://oss.maxcdn.com/html5shiv/3.7.2/html5shiv.min.js"></script>
<script src="https://oss.maxcdn.com/respond/1.4.2/respond.min.js"></script>
<![endif]-->
```
- Crear /views/layouts el partial _header_javacript.html.erb
```sh
<!-- Letras de la aplicacion -->
<link href='http://fonts.googleapis.com/css?family=Niconne' rel='stylesheet' type='text/css'>
<link href='http://fonts.googleapis.com/css?family=Great+Vibes' rel='stylesheet' type='text/css'>
```
- Modificar el layo de la aplicación para que contenga los partials anteiores
```sh
<!DOCTYPE html>
<html lang="en" dir="ltr">
  <head>
    <%= render 'layouts/metas' %>
    <%= render 'layouts/favicon' %>

    <title>Fitness Notes</title>

    <%= stylesheet_link_tag 'application', media: 'all', 'data-turbolinks-track' => true %>
    <%= csrf_meta_tags %>

    <%= render 'layouts/shim' %>
    <%= render 'layouts/header_javascript' %>
  </head>
  <body>
    <header>
      <%= render 'layouts/navigation' %>
    </header>
    <main class="container theme-showcase" role="main">
      <div class="jumbotron">
        <%= render 'layouts/messages' %>
        <%= yield %>
      </div>
    </main>
    <%= render 'layouts/footer' %>
    <%= javascript_include_tag 'application', 'data-turbolinks-track' => true %>
  </body>
</html>
```
- En caso de desearse un tema de Bootwatch, crear en /assets/stylesheets el archivo bootwatch.css.scss con toda la configuracion del tema elegido
- Para los estilos propios de la aplicacion, crear en /assets/stylesheets el archivo zzcustom.css.scss
- Confirmar cambios en la rama
```sh
RAILS_ENV=production rake assets:precompile 
git branch
git status
git add -A
git commit -m "Layout"
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
git push heroku
heroku open
```  
- La rama auxiliar se podria eliminar
```sh
git branch
git -d <nombre rama aux>
```  

---











```sh

```  