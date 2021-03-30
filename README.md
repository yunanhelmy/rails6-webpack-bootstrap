# About

This is example of Rails project using bootstrap

# Dependencies

- ruby 3.0.0
- rails 6.1
- postgresql
- bootstrap 4

# Install Rails

Create new project

```
rails new my-project -d postgresql
```

Go to current directory

```
cd my-project
```

Setup database

```
rails db:create db:migrate
```

# Install bootstrap

```
yarn add bootstrap jquery popper.js
```

Configure jquery in webpack `config/webpack/environment.js`

```
const webpack = require('webpack')
environment.plugins.append(
  'Provide',
  new webpack.ProvidePlugin({
    $: 'jquery',
    jQuery: 'jquery',
    Popper: ['popper.js', 'default']
  })
)
```

Import bootstrap and jquery

```
import $ from 'jquery'
import 'bootstrap/dist/js/bootstrap'
```

# Create dummy page

Create new controller

```
rails g controller welcome index
```

Set root in `config/routes.rb`

```
root 'welcome#index'
```

# Configure css

Create css entry point `app/javascript/stylesheets/application.scss`

Import bootstrap

```
@import '~bootstrap/scss/bootstrap';
```

Import css entry point in `app/JavaScript/packs/application.js`

```
import '../stylesheets/application'
```

# Load javascript and css from webpack

In `app/views/layout/application.html.erb`

```
<%= stylesheet_pack_tag 'stylesheets/application', media: 'all', 'data-turbolinks-track': 'reload' %>
<%= javascript_pack_tag 'application', 'data-turbolinks-track': 'reload' %>
```

# Running project

```
rails s
```

check http://localhost:3000

# Using foreman

```
gem install foreman
```

# Configure foreman

In Procfile.dev

```
web: bundle exec puma -C config/puma.rb -p 3000
webpacker: ./bin/webpack-dev-server
```

# Running project with foreman

```
foreman start -f Procfile.dev
```
