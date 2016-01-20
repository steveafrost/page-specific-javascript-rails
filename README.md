# Page Specific Javascript Rails

## Objectives

1. How to Write Page-Specific JS
2. Loading Page-Specific JS in the Manifest
3. Loading Page-Specific JS through javascript_include_tag
4. Creating a content_for page specific JS and writing JS in partials.

## Outline

The first thing about page specific js is that there really shouldn't be too much of that. write page specific js as units in js files that may or may not correlate to a page, controller, or action, but rather are grouped functionally or through objects in single js files.

You might have a app/assets/users.js file that relates to functionality for the user's account, like behavoirs for their profile page or adds special links to their avatar, but in reality, that JS should be loaded once on the initial page load and then just used in the rest of the application.

So the first thing is to learn to write page specific js but still include it in the manifest.

## Page Specific JS in a manifest

you might have a products.js that controls behaviors on product card units, like hovers or drop downs or ajax submissions, but that should all be written in products.js, products.js should be loaded in the main manifest, and then you just have a $(ready) in products.js that only fires against DOM elements that are either present or not. So no page specific js, just write it agnostic to the page and load it all in the main manifest.

## Page Specific JS with individual javascript_include_tag

Should you need a little snippet of JS that is very page or layout specific, just write it in app/assets and then include that in the different layout.

## A content_for

For truely page specific javascript the best thing to do is add a content_for :js block in your layout (either in head or below the body)

application.html.erb

```
<head>
  <meta>
  <%= javascript_include_tag 'application' %>
  <%= yield :js %>
```

Then in your view

app/views/products/show.html.erb

```
<% content_for :js do %>
<script>
 Some Page specific JS
</script>
<%= javascript_include_tag 'products' %>
<% end %>
```

That's a great pattern for getting page specific JS. You can even load another manifest there or render a partial with JS.

In general the pattern should be to write it agnostically and include an application wide manifest.
