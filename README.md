# Rails Yield Readme

## Objectives

1. Explain what a `yield` statement in `application.html.erb` does and why we use it
2. Implement a yield statement in `application.html.erb`

## Layout

If you look at pretty much every website, you'll notice that there are things that exist across all of the site's pages. Typically, the navigation bar and the footer content stay the same. There may also be menu options that stay consistent across all pages.

You could copy and paste the HTML and ERB for nav bar and make sure that code is in every single erb file, but that isn't at all DRY.

In order to not repeat ourselves, we can create a single file, `application.html.erb`, that contains all of the code we want to exist on every single web page.

Below is the HTML for a website that has a header and links to JavaScript files.

```erb
<!doctype html>
<html>
  <head>
    <title>Cats</title>
    <%= stylesheet_link_tag 'https://maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css' %>
    <%= stylesheet_link_tag 'application', 'data-turbolinks-track': 'reload' %>
    <%= csrf_meta_tags %>
    <%= csp_meta_tag %>
  </head>
  <body>

    <div class="container">
      <h1>I love cats</h1>
      <img src="https://s3.amazonaws.com/after-school-assets/cat-typing.gif">



    </div>
    <%= javascript_include_tag 'https://ajax.googleapis.com/ajax/libs/jquery/1.11.1/jquery.min.js' %>
    <%= javascript_include_tag 'https://maxcdn.bootstrapcdn.com/bootstrap/3.2.0/js/bootstrap.min.js' %>
    <%= javascript_include_tag 'application', 'data-turbolinks-track': 'reload' %>
  </body>
</html>
```

We want every page to have a `<head>` tag with links to Bootstrap's and our own CSS files. The body of our site contains the heading `I love cats` and a cat gif. At the bottom, we have our jQuery and Bootstrap links.

Now, let's say we have an `index.html.erb` with the following code:

```html
<h2>This cat...</h2>
<img src="https://s3.amazonaws.com/after-school-assets/cat.gif" />
```

### Yield

Now that we have our layout written, how can we get the `application.html.erb` loaded around the `index.html.erb`?

This is where the `yield` comes in.

In `application.html.erb`, we need to add a `yield` wherever we want the other page content to be loaded:

```erb
<!doctype html>
<html>
  <head>
    <title>Cats</title>
    <%= stylesheet_link_tag 'https://maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css' %>
    <%= stylesheet_link_tag 'application', 'data-turbolinks-track': 'reload' %>
    <%= csrf_meta_tags %>
    <%= csp_meta_tag %>
  </head>
  <body>

    <div class="container">
      <h1>I love cats</h1>
      <img src="https://s3.amazonaws.com/after-school-assets/cat-typing.gif">

      <%= yield %>



    </div>
    <%= javascript_include_tag 'https://ajax.googleapis.com/ajax/libs/jquery/1.11.1/jquery.min.js' %>
    <%= javascript_include_tag 'https://maxcdn.bootstrapcdn.com/bootstrap/3.2.0/js/bootstrap.min.js' %>
    <%= javascript_include_tag 'application', 'data-turbolinks-track': 'reload' %>
  </body>
</html>
```

Let's say we have a controller action:

```ruby
def index
  # action logic here
end
```

When the above controller action is triggered and Rails renders the view, it looks to see if there is a layout file titled `application.html.erb`. If that file exists, it loads that content around the desired view file, in this case `index.html.erb`.

The resulting HTML will look like this:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Cats</title>
    <link
      rel="stylesheet"
      href="https://maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css"
    />
    <link rel="stylesheet" href="/assets/application-[hash].css" />
  </head>
  <body>
    <div class="container">
      <h1>I love cats</h1>
      <img src="https://s3.amazonaws.com/after-school-assets/cat-typing.gif" />

      <h2>This cat...</h2>
      <img src="https://s3.amazonaws.com/after-school-assets/cat.gif" />
    </div>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.1/jquery.min.js"></script>
    <script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.2.0/js/bootstrap.min.js"></script>
    <script src="/assets/application-[hash].js"></script>
  </body>
</html>
```

## Does this need an update?

Please open a [GitHub issue](https://github.com/learn-co-curriculum/phrg-rails-yield-readme/issues) or [pull-request](https://github.com/learn-co-curriculum/phrg-rails-yield-readme/pulls). Provide a detailed description that explains the issue you have found or the change you are proposing. Then "@" mention your instructor on the issue or pull-request, and send them a link via Connect.

<p data-visibility='hidden'>PHRG Rails Yield Readme</p>
