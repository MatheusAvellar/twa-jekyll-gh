# Twemoji Awesome for Jekyll & GitHub Pages

The Twemoji plugin for Jekyll, working on GitHub Pages.

I'll cut to the chase and tell you how to use it. If you'd like
to know more about the project, scroll further down for some
context and how it works.


## How to use

1. Download `twemoji.html` and put it in your `_includes/` folder;
2. Download *either* the `.css` *or* the `.scss` file and put it in your `assets/` folder;
3. Link the CSS file in your HTML. For example, in `_includes/head.html`:
```html
<link rel="stylesheet" href="{{ "/assets/twemoji-awesome.css" | relative_url }}">
```
4. On pages where you want to use a twemoji, add `{%- include twemoji.html -%}` to the top;
5. Wherever you'd like to add an emoji, simply type `{{ twa-pizza }}` (where "pizza" is the emoji name).

Here's some example code and output:

```markdown
{%- include twemoji.html -%}

**Output**:
Buy me some {{ twa-pizza }} please!
```

![Screenshot of the output: the emoji renders beautifully.](https://i.imgur.com/VTXDUdn.png)


## Context

[@ellekasai](https://github.com/ellekasai) has an amazing project,
called [Twemoji Awesome](https://github.com/ellekasai/twemoji-awesome).
It's meant to be used on the web, similarly to [Font Awesome](https://fontawesome.com/),
but, instead of icons, it renders [Twemoji](https://twemoji.twitter.com).
To insert a heart emoji, one would do `<i class="twa twa-heart"></i>`.

Then, [@Ezmyrelda](https://github.com/Ezmyrelda) built a plugin for Jekyll
to implement Twemoji Awesome (you can find it [here](https://github.com/Ezmyrelda/twa)).
That way, when you write `{% twa twa-heart %}`, it inserts a heart emoji.

However, GitHub Pages is a big fan of vanilla Jekyll: **it does not like
many plugins**. You can check the entire 47-item-long list of plugins
supported by GitHub pages [right here](https://pages.github.com/versions/).

If you decide to be stubborn and install an unlisted plugin anyway, this is
a sample of what happens:

![Screenshot of error GitHub displays: "The tag is not recognized"](https://i.imgur.com/cGgbsuo.png)

In short, you really can't use it.

You may have gathered by now that I was trying to use Twemoji Awesome,
with Jekyll, on GitHub Pages. And GitHub was having none of it.


## How it works

What I've decided to do, instead of writing a plugin, is to use
[Liquid](https://github.com/Shopify/liquid) markup to define a crap-ton of
variables. So, for every emoji name in the JSON lists in the
[twemoji-possum](https://github.com/kamalasaurus/twemoji-possum/) repository,
there's a line in `twemoji.html` as follows:

```html
{% assign twa-pizza = '<i class="twa twa-pizza"></i>' %}
```

That way, you can simply use `{{ twa-pizza }}`, and it'll insert the markup
automatically. I assume there's no overhead in defining a ton of variables
if you don't use all of them; the 'compiler' should just ignore anything
that isn't used, thus not increasing the size of the built pages.

The catch is that, for that simple markup to work, you must include
`twemoji.html` on every page you intend to use an emoji. I might be wrong
about this, but from my early testing, it seems to be that way.