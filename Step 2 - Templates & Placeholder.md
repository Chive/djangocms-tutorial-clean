Step 2 - Templates & Placeholders
=================================

In this part of the tutorial we're going to tell you a thing or two about (static) placeholders and we're also going to show how you can make your own HTML templates CMS ready.

About templates
---------------

You can use HTML templates to customize the look of your website, define placeholders to mark sections which can be edited through your browser and use special tags to render stuff like the menu and more. You can define multiple templates (e.g. one where the content spans the whole page and another one where there is a sidebar) and switch between them from the toolbar.

What are placeholders?
---------------------

```html
{% placeholder "content" %}
```

Placeholders are an easy way to define sections in HTML code to be editable through our frontend editing. They mark the part of the page which are actually content:

```html
{% load cms_tags %}
<html>
    <head>
        <title>My Awesome Website</title>
    </head>
    <body>
        {% block content %}
            {% placeholder "content" %}
        {% endblock %}
    </body>
</html>
```

> **Note:** If you know django, you've probably seen the block-tag before (`{% block "content" %}{% endblock "content" %}`). If not, you should head over to [the django docs and read about it.](https://docs.djangoproject.com/en/dev/topics/templates/)

> **Note:** The block tag is not strictly necessary in the example. It is only there for extensibility.

We already put this into the templates which you've installed previously with the installer. Feel free to open one of the templates and have a look at them and add some content.


Static Placeholders
-------------------

A placeholders content is different for every page. But let's say you want to have a section on your website which should be the same on every single page you use a template with that placeholder, e.g. a footer block. It would be nice if you could edit your footer through your browser, but not if you had to fill in the content on every single page.

That's why there are static placeholders.

Static placeholders are an easy way to display the same content on multiple locations on your website. Static placeholders act almost like normal placeholders, except for the fact that once a static placeholder is created and you added content to it, it will be saved globally. Even when you remove the static placeholders from a template, you can reuse them later.

You can use a template tag to display a placeholder in a template without the need for an actual placeholder in your models:

```python
{% load cms_tags %} {% static_placeholder "footer" %}
```

Let's create a footer!
----------------------

But that's theory, let's implement a footer!

Since we want our footer on every single page, we should add it to our base template (`src/templates/base.html`). Open it up and add a new static_placeholder (e.g. `footer`) at the bottom of the html body (or wherever you want it to be, you don't have to obey some piece of text!).

```python
<footer>
  <hr/>
  {% static_placeholder 'footer' %}
</footer>
```


Save the template and go back to your browser. Change to draft and then structure mode and fill in content into your footer! After you've saved it, go check out the other pages on your websites to see that the footer appears there too!


Rendering Menus
---------------

In order to render the CMS' menu in your template you can use the [`show_menu`](http://docs.django-cms.org/en/develop/getting_started/navigation.html#show-menu) tag.

Here's a basic example:
```html
{% load menu_tags %}
<ul>
    {% show_menu 0 100 100 100 %}
</ul>
```

If you chose "bootstrap" while setting up with djangocms-installer, the menu will already be there and ``templates/menu.html`` will already contain a version that uses bootstrap compatible markup.

You should definitely check out the CMS' documentation on [navigation, menus and breadcrumbs](http://django-cms.readthedocs.org/en/latest/basic_reference/navigation.html).

[In step 3 we're going to talk about CMS Plugins!](https://github.com/Chive/djangocms-tutorial/blob/master/Step%203%20-%20CMS%20Plugins.md)
