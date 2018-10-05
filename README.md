
基本功能的制作方法：
```
cd newspace
ls
rails new blog
cd blog
rails s
atom .
git init
git add .
git commit -m "first commit"
```
```
clear
rails g controller posts
```
config/routes.rb
```
Rails.application.routes.draw do
  resources :posts
  root 'posts#index'
end

```

touch app/views/posts/index.erb
```
<h1>this is index.erb file ...</h1>
```
rails s
touch app/views/posts/new.erb
```
<h1>New Post</h1>

<%= form_for :post, url: posts_path do |f| %>
   <p>
     <%= f.label :title %><br>
     <%= f.text_field :title %>
    </p>

    <p>
      <%= f.label :body %><br>
      <%= f.text_field :body %>
    </p>

     <p>
      <%= f.submit %>
      </p>
<% end %>

```
```
rails g model Post title:string body:text
rake db:migrate
```
```
app/controllers/posts_controller.rb
```
class PostsController < ApplicationController
  def index
  end


  def new
  end

  def create
    @post = Post.new(post_params)
    @post.save

    redirect_to @post
  end


private
   def post_params
     params.require(:post).permit(:title, :body)
   end
end

```
touch app/views/posts/show.erb
```
<h1 class="title">
 <%= @post.title %>
</h1>

<p class="date"></p>
submitted<%= time_ago_in_words(@post.created_at) %> Age

<h1 class="body">
 <%= @post.body %>
</h1>

<%= link_to "New Post", new_post_path, class:"button" %>
<%= link_to "Back", posts_path, class:"button" %>

```
app/controllers/posts_controller.rb
```
class PostsController < ApplicationController
  def index
  end


  def new
  end

  def create
    @post = Post.new(post_params)
    @post.save

    redirect_to @post
  end

  +def show
   +@post = Post.find(params[:id])
  +end

private
   def post_params
     params.require(:post).permit(:title, :body)
   end
end

```
app/controllers/posts_controller.rb
```
class PostsController < ApplicationController
  +  def index
  +    @posts = Post.all.order('created_at DESC')
  +  end


  def new
  end

  def create
    @post = Post.new(post_params)
    @post.save

    redirect_to @post
  end

  def show
   @post = Post.find(params[:id])
  end

private
   def post_params
     params.require(:post).permit(:title, :body)
   end
end

```
app/views/posts/index.erb
```
<% @posts.each do |post| %>
<div class="post_wrapper">
  <h2><%= link_to post.title, post %></h2>
  <p class="date"><%= post.created_at.strftime("%B, %d, %Y") %>
</div>
<% end %>

```

git status
git add .
git commit -m "add posts"
```
