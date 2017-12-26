Title: Rails5で取り込まれる予定のrails-apiを使ってWeb APIをつくる
Date: 2015-10-31 19:54
Author: waura
Category: Ruby on Rails
Tags: Rails, Ruby
Slug: rails-api_sample
Status: published

## はじめに  
web apiを作るのに特化したrails-apiを使ってweb apiを作ってみます。  
[rails-api](https://github.com/rails-api/rails-api)は、Rails5で取り込まれる予定みたいです。  
rails-apiは、web
apiを作るだけなら不要なrails要素を省いてアプリを作成することができます。  
Web
APIオンリーでフロントエンドは、別のフレームワーク等を使って開発する場合などに使用すると良いのではないでしょうか。  
今回は、問い合わせるとjsonを返すだけの単純なGETメソッドのAPIを作成してみます。

## rails-apiのインストール  
```  
$ gem install rails-api  
```

## rails-apiのディレクトリを作成  
今回は、sample_apiという名前で作成してみました。

```  
$ rails-api new sample_api  
```

## ModelとControllerの作成  
rails-apiでは、Viewを使わないのでModelとControllerだけ作成します。  
ここでは、Model名とController名はそれぞれBookとbooksとしておきます。  
自分で作成する場合は、好きな名前にしてください。

### Modelの作成

```  
$ ./bin/rails g model Book name:string  
$ ./bin/rake db:migrate  
```

### Controllerの作成  
Controllerは、バージョニングできるようにバージョン名でディレクトリを振り分けて配置しています。

```  
$ ./bin/rails g controller api/v1/books  
```

```ruby
# app/controllers/api/v1/books_controller.rb  
class Api::V1::BooksController \< ApplicationController  
  def index  
    @indicators = Indicator.all  
    render json: @indicators  
  end  
end  
```

## ルーティングの設定  
```ruby
# config/routes.rb  
Rails.application.routes.draw do  
  namespace :api, {format: \'json\'} do  
    namespace :v1 do  
      resources :books  
    end  
  end  
end  
```

## テスト用データの登録  
rake db:seedを使ってテスト用のデータを登録します。

```ruby  
# db/seed.rb  
Book.create(name: \"test name\")  
```

```  
$ ./bin/rake db:seed  
```

## テストサーバーの起動  
```  
$ ./bin/rails server  
```

サーバーを起動した後、  
[http://localhost:3000/api/v1/books](http://localhost:3000/api/v1/books)  
にアクセスすればテスト用のデータとして登録していた内容がjsonとして返されます。
