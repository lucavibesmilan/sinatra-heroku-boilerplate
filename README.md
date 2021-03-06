# Sinatra Application Boilerplate for Heroku

A simple boilerplate `sinatra` application skeleton for quick deployment to Heroku.


## Libraries

* [http://getbootstrap.com/][1]
* [http://glyphicons.getbootstrap.com/][2]
* [http://fontawesome.io/][3]
* [http://bourbon.io/][4]
* [http://retinajs.com/][5]

## Requirements

* Default ruby version is `1.9.3-p448` via `rbenv`

## Installation
Example app runs at [Heroku][0]

Clone the repo

    git clone https://github.com/webBoxio/sinatra-heroku-boilerplate.git my-sinatra-app
    git remote remove origin # remove default origin

add your own repo ( _origin_ )

    git remote add orgin YOUR_REPO_URL
    # git push -u origin master

You can install required `gem` files via;

    bundle install --path vendor/bundle

or you can use rake task;

    rake install

You can define your **Amazon S3 Bucket** information and **Google Analytics ID**
in the `config/prefs.yml`. Use the `<%= @s3_prefix %>` tag in your templates aka `views`

    s3_bucket: sinatra-heroku-boilerplate
    s3_path: /public
    sync_path: public/
    google_analytics_id: UA-6463685-31

this example is a working example...

## Warning for S3 Usage

Please don't forget to add you `public/` folder to `.gitignore` if you push
all your static files to S3 Bucket. If not your Heroku slug file will grow
and it is not wanted! (:

Example data generates `http://sinatra-heroku-boilerplate.s3-us-west-2.amazonaws.com/public/` as prefix. Put
all your static data you Amazon S3. Example usage `views/layout.erb`:

    <link rel="stylesheet" href="<%= @s3_prefix %>/vendor/bootstrap3/glyphicon/bootstrap-glyphicons.css">

When you are running development server via `rake` or `rake run:development` it
generates an empty string for `<%= @s3_prefix %>` and example above becomes:

    <link rel="stylesheet" href="/vendor/bootstrap3/glyphicon/bootstrap-glyphicons.css">

Also, for example, you have image files under `public/images` and you want to use
S3 support.

    <img src="<%= @s3_prefix %>/images/icons/apple-touch-icon-144-precomposed.png" />

will become ( _depending on your prefs.yml_ );

    <img src="http://sinatra-heroku-boilerplate.s3-us-west-2.amazonaws.com/public/images/icons/apple-touch-icon-144-precomposed.png" />

on production mode...

![Example Image](http://sinatra-heroku-boilerplate.s3-us-west-2.amazonaws.com/public/images/icons/apple-touch-icon-144-precomposed.png)

and uses your local `public/` folder. You can run server in a production mode via
`rake run:production`. Don't forget, google analytics code will be shown only
in **production** mode.

You can display all the rake tasks via `rake -T`

## SASS and SCSS Usage

You can both use `sass` and `scss`... Put **sass** files to `sass/` with `.sass` extension or put
**scss** files to `scss/` with `.scss` extension. Default skel comes with `scss` and **bourbon** included.

`views/layout.erb` :

    <link href="/scss/application.scss" rel="stylesheet" />

## Test Your Server

You can use `foreman`.

    foreman start # or use built-in rake task
    rake run:unicorn

open [http://localhost:5000](http://localhost:5000)

## Deploy to Heroku

Create a Heroku app:

    heroku apps:create
    # you can give whatever name you like to
    # heroku apps:rename NAME_OF_YOUR_APP
    git push heroku


[0]: http://sinatra-heroku-boilerplate.herokuapp.com/ 
[1]: http://getbootstrap.com/
[2]: http://glyphicons.getbootstrap.com/
[3]: http://fontawesome.io/
[4]: http://bourbon.io/
[5]: http://retinajs.com/