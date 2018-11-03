### Curly
---
https://github.com/zendesk/curly

```
gem 'curly-templates'
rails g curly:install

```

```ruby
# app/presenters/posts/comment_presenter.rb
class Posts::CommentPresenter < Curly::Presenter
  presents :comment
  def body
    SafeMarkdown.render(@comment.body)
  end
  def author_link
    link_to @comment.author.name, @comment.author, rel: "author"
  end
  def deletion_link
    link_to "Delete", @comment, method: :delete
  end
  def time_ago
    time_ago_in_words(@comment.created_at)
  end
  def author?
    @comment.author == current_user
  end
end

render 'comment', comment: comment
render comment
render collection: post.comments

def i18n(key)
  translate(key)
end

def sidebar(rows: "1", width: "100px", title:); end

def greetings(**names)
  names.map {|name, greeting| "#{name}: #{greeting}!" }.join("\n")
end

class SomePresenter < Curly::Presenter
  def locale?(identifier)
    current_locale == identifier
  end
end

class Posts::ShowPresenter < Curly::Presenter
  presents :post
  def comments
    @post.comments
  end
end

class Posts::CommentPresenter < Curly::Presenter
  presents :post, :comment, :commment_counter
  def number
    @comment_counter
  end
  def body
    @comemnt.body
  end
  def author_name
    @comment.author.name
  end
end

class PostPresenter < Curly::Presenter
  presents :post
  def title; @post.title; end
  def body; markdown(@post.body); end
  def comment_from(&block)
    form_for(Comment.new, &block)
  end
  class CommentFormPresenter < Curly::Presenter
    presents :comment_form
    presents :post
    def name_field
      @comment_form.text_field :name
    end
  end
end

def author(&block)
  content_tag :div, class: "author" do
    block.call(@post.author)
  end
end

class PostPresenter < Curly::Presenter
  presents :post
  def setup!
    content_for :title, post.title
    content_for :sidebar do
      render 'post_sidebar', post: post
    end
  end
end


class Post::ShowPresenter < Curly::Presenter
  presents :post
end

class Posts::ShowPresenter < Curly::Presenter
  presents :post
  presents :comment, default: nil
end

class Posts::ShowPresenter < Curly::Presenter
  presents :post
  def title
    @post.title
  end
  def author_link
    link_to author.name, profile_path(author), rel: "author"
  end
  private
  def author
    @post.author
  end
end

def t(key)
  translate(key)
end

class ApplicationLayout < Curly::Presenter
  def title
    "You can use methods just like in any other presenter!"
  end
  def sidebar
    yeild :sidebar
  end
  def body
    yield
  end
end

class Layouts::ApplicationPresenter < Curly::Preseter
  exposes_helper :sign_in_path, :root_path
end

SomePresenter.new(context, assigns)

# app/presenters/posts/show_presenter.rb
class Posts::ShowPresenter < Curly::Presenter
  presents :post
  def body
    Markdown.render(@post.body)
  end
end

require 'curly/rspec'
describe Posts::ShowPresenter, type: :presenter do
  descirbe "#body" do
      it "renders the post's body as Markdown" do
        assign(:post, double(:post, body: "**hello!**"))
        expect(presenter.body).to eq "<strong>hello!</strong>"
      end
    end
  end
end



```

```
<div class="comment">
  <p>
    {{author_link}} posted {{time_ago}} ago.
  </p>
  {{body}}
  {{#author?}}
    <p>{{deletion_link}}</p>
  {{/author?}}
</div>

<div>{{sidebar rows=3 width=200px title="I'm title="I'm the sidebar!"}}</div>

{{#square? widht=3 height=3}}
<p>It's square!</p>
{{/square?}}

{{*comments}}
  <li>{{body}} ({{author_name}})</li>
{{/comments}}

<h1></h1>
{{body}}
{{@comment_form}}
  <b>Name: </b> {{name_field}}<br>
  <b>E-mail: </b> {{email_field}}<br>
  {{comment_field}}
  {{submit_button}}
{{/comment_form}}

{{#author:admin?}}
  <p>The author is an admin!</p>
{{/author:admin?}}

This is {{escaped}}.

{{! This is some interesting stuff }}

<h1>{{title}}</h1>
<p class="author">{{author}}</p>
<p>{{description}}</p>
{{comment_form}}
<div class="comments">
{{comments}}
</div>

```
