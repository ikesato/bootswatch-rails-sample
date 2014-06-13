bootswatch + rails 手順
=======================

1. rails インストール

 ```````````````````
 $ gem install rails
 ```````````````````

2. rails プロジェクト作成

 ````````````````````````````
 $ rails new bootstrap-sample
 ````````````````````````````

3. Install therubyracer

 以下 Gemfile に追加して bundle を実行する
 ``````````````````
 gem 'therubyracer'
 ``````````````````


4. Install rspec (ここは任意)

 Gemfile に追加
 `````````````````````````````````
 group :development, :test do
   gem 'rspec-rails', '~> 3.0.0'
 end
 `````````````````````````````````

 以下実行
 `````````````````````````````````
 $ bundle
 $ rails generate rspec:install
 $ bundle binstubs rspec-core
 $ rm -fr test
 $ rspec
 `````````````````````````````````

4. scaffold
 ````````````````````````````````````````````````````````````````````
 rails generate scaffold book title:string author:string outline:text
 rake db:migrate
 ````````````````````````````````````````````````````````````````````

5. Install bootswatch
 Gemfile に追加

 ````
 # twitter bootstrap css & javascript toolkit
 gem 'twitter-bootswatch-rails', '~> 3.1.1'
 
 # twitter bootstrap helpers gem, e.g., alerts etc...
 gem 'twitter-bootswatch-rails-helpers'
 ````

 以下実行。テーマは "readable" にした。
 ```
 $ bundle
 $ rails g bootswatch:install readable
 $ rails g bootswatch:import readable
 $ rails g bootswatch:layout readable
 ```

6. config/initializers/assets.rb を新規追加して以下を追加
 ````````````````````````````````````````````````````````````````
 Rails.application.config.assets.precompile += %w( readable.css )
 Rails.application.config.assets.precompile += %w( readable.js )  
 ````````````````````````````````````````````````````````````````

7. 以下実行

 ```
 cp app/views/layouts/readable.html.erb app/views/layouts/application.html.erb
 vi app/views/layouts/application.html.erb
 ```

 <%= yeild %>
 の位置が変なので、 class="container theme-showcase" の後に置く。

  `````````````````````````````````````````
  <div class="container theme-showcase">
    <%= yield %>
  ...
  `````````````````````````````````````````

8. スタイルシートが変なので以下追加

 ``````````````````````````````````````
 vi app/assets/stylesheets/readable.css
 ``````````````````````````````````````

 ```````````````````````````````````````````````
 .theme-showcase {
   margin-top: 50px;
 }
 ```````````````````````````````````````````````


9. 既存のレイアウトをテーマ化する
 rails g bootswatch:themed Books

10. 完了
