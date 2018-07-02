## 1. devise 사용하기

gemfile

```ruby
gem 'devise'
```



routes.rb

```ruby
Rails.application.routes.draw do
  root 'home#index'
end
```

```ruby
$ bundle install
$ rails g devise:install
```



config > environments > development.rb

```ruby
  # Don't care if the mailer can't send.
  config.action_mailer.raise_delivery_errors = false
  config.action_mailer.perform_caching = false
  config.action_mailer.default_url_options = {host: 'localhost', port: 3000 } #얘 추가
```



app > views > layouts > application.html.erb

```ruby
  <body>
    <p class="notice"><%= notice %></p>
    <p class="alert"><%= alert %></p>
    <%= yield %>
  </body>
```

```ruby
$ rails g devise users
#db뿐만 아니라 routes.rb에 devise_for :users도 추가된걸 볼 수 있음
$ rake db:migrate
```



app > views > home > index.html.erb

```ruby
<h1>Welcome!</h1>

<!-- 로그인 상태 시 -->
<% if user_signed_in? %>
    <%= current_user.email %>
    <%= link_to '로그아웃', destroy_user_session_path, method: "delete" %>
<% else %>
<!-- 로그아웃 상태 시 -->
    <%= link_to '로그인', new_user_session_path %> <!--기본이 get -->

<% end %>
```

```ruby
rails g devise:views
```

views > shared > _links.html.erb(딱히 바꿀 코드는 없음. 그냥 참고용)

```ruby
<%- if controller_name != 'sessions' %> 는 
<%- params[:controlelr] != 'sessions' %>와 같음

여기서 <%- 의 의미는
```

```ruby
<%- if devise_mapping.omniauthable? %>
# https://github.com/zquestz/omniauth-google-oauth2 를 들어가보면, 
```

```ruby
$ rails g devise:views
$ rails g devise:controllers
$ rails g devise:controllers users
```

```ruby
class Users::SessionsController < Devise::SessionsController에서 <는 상속
```

