---
layout: post
title:  "How to structure your meteor app"
date:   2015-08-08 09:48:00
categories: meteor
---

# Major goals of structuring your meteor app
- Another developer should be able to understand your app structure in a
  short amount of time.
- When you see some code, e.g. a function call, you should be able to know the
  location of the file that contains the definition of the code immediately.
- Your files should be small.
- You should be able to easily reason the loading order of your app.
- A global namespace and its methods should be confined into one folder or one
  file.

# The recommend structure
- before/
  - lib/
    - before/
    - schemas/
- client/
  - autoruns/
  - components/
  - config/
  - lib/
  - routes/
  - stylesheets/
  - template-helpers/
    - index.html
    - router.js
    - subscriptions.js
- collection-helpers/
- methods/
- private/
- public/
- server/
  - authorizations/
  - factories/
  - lib/
  - methods/
  - publications/
  - router.js


{% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}

You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. You can rebuild the site in many different ways, but the most common way is to run `jekyll serve`, which launches a web server and auto-regenerates your site when a file is updated.

To add new posts, simply add a file in the `_posts` directory that follows the convention `YYYY-MM-DD-name-of-post.ext` and includes the necessary front matter. Take a look at the source for this post to get an idea about how it works.

Jekyll also offers powerful support for code snippets:

{% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}

Check out the [Jekyll docs][jekyll] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll’s dedicated Help repository][jekyll-help].

[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help
