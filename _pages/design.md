---
layout: main_guide
title: HTML と CSS を使ってデザインしてみよう
permalink: design
---

# HTML & CSS を使ってデザインしてみよう

*Created by Alex Liao, [@alexliao](http://bannka.com/alex), Translated by Hiroshi SHIBATA [@hsbt](http://twitter.com/hsbt)

{% include main-guide-intro.html %}

アプリケーションは完成しましたが、まだ scaffold で自動生成した状態です。いくつかのデザインを追加してよく見かける Web サイトのようにしてみましょう。このチュートリアルが終わった時に、あなたのアプリケーションは[この](http://railsgirlsapp.herokuapp.com/ideas)ようになるはずです。

## Style the idea list page

The default Rails scaffolding allow us to build pages very quickly and get our app working. The design could use some work. For this we're going to be using [Bootstrap](https://getbootstrap.com/docs/5.2/) again. We'll be using some existing Bootstrap classes to make our own components, style links and buttons.

`app/views/ideas/index.html.erb` を開いて以下の内容に置きかえます。

{% highlight erb %}
<p style="color: green"><%= notice %></p>

<h1>Ideas</h1>
<%= link_to "Add a new idea", new_idea_path, class: "btn btn-primary mb-3" %>

<div class="list-group w-auto">
  <% @ideas.each do |idea| %>
    <%= render idea %>
  <% end %>
</div>
{% endhighlight %}

This alone isn't all the styling we'll need, but this will show all the ideas in a nice list in a moment. At the top we'll have a new blue button with the label "Add a new idea".

Open `app/views/ideas/_idea.html.erb` in your Text Editor and replace all the lines with these lines:

{% highlight erb %}
<div id="<%= dom_id idea %>" class="list-group-item list-group-item-action d-flex gap-3 py-3">
  <div class="d-flex flex-column gap-2 w-100">
    <h2><%= link_to idea.name, idea_path(idea) %></h2>
    <p><%= idea.description %></p>
    <small class="opacity-50 text-nowrap">Last updated <%= time_ago_in_words idea.updated_at %></small>
  </div>
  <%= image_tag(idea.picture_url, width: 150, height: 150, class: "img-thumbnail flex-shrink-0") if idea.picture? %>
</div>
{% endhighlight %}

This will style each idea in the list to show their idea name as a link to the idea itself, it shows when the idea was last updated, the idea description and a thumbnail of the picture you uploaded.

Visit the <http://localhost:3000/ideas> page to see your new idea app design.

{% coach %}
Explain how the design works line by line. What is HTML, what is CSS and what parts are Bootstrap?
{% endcoach %}

## Style the idea detail page

idea のタイトルをクリックすると、idea の詳細画面を見ることができます。今はまだ Rails によって作られた scaffold ページのままです。さあ、これをもっとよくしてみましょう。

`app/views/ideas/show.html.erb` をテキストエディタで開いて、以下の内容で全てを置きかえます。

{% highlight erb %}
<p style="color: green"><%= notice %></p>

<div id="<%= dom_id @idea %>" class="d-flex gap-3 py-3">
  <div class="d-flex flex-column gap-2 w-100">
    <h1><%= @idea.name %></h1>
    <p><%= @idea.description %></p>
    <small class="opacity-50 text-nowrap">Last updated <%= time_ago_in_words @idea.updated_at %></small>
  </div>
  <%= image_tag(@idea.picture_url, width: 150, height: 150, class: "img-thumbnail flex-shrink-0") if @idea.picture? %>
</div>

<div class="d-flex gap-3 py-3">
  <%= link_to "Edit this idea", edit_idea_path(@idea), class: "btn btn-primary" %>
  <%= link_to "Back to ideas", ideas_path, class: "btn btn-outline-secondary" %>
  <%= button_to "Destroy this idea", @idea, method: :delete, class: "btn btn-danger", form: { data: { turbo_confirm: "Are you sure?" } } %>
</div>
{% endhighlight %}

The new page should look a lot better and a lot like how the ideas are shown on the index page. The actions you can perform on the idea now also are shown in highly visible buttons below the idea details.

{% coach %}
Explain how the design works line by line. What is HTML, what is CSS and what parts are Bootstrap?
{% endcoach %}

## References

To style the pages we've used the following Bootstrap components. Check out the documentation to learn more.

- [Bootstrap list groups](https://getbootstrap.com/docs/5.2/components/list-group/)
- [Bootstrap buttons](https://getbootstrap.com/docs/5.2/components/buttons/)
- [Bootstrap images](https://getbootstrap.com/docs/5.2/content/images/)

## What next?

Did the design and styling catch your eye? Do you want to unleash your inner designer and style more pages?

* Use your new knowledge to design the new idea form located at `app/views/ideas/_form.html.erb`
* Add more design to the other pages as you wish.
