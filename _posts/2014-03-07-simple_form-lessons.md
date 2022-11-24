---
layout: post
title:  "simple_form lessons"
date:   2014-03-07 06:32:41
image: IMG_6454.png
image_thumb: IMG_6454_thumb.png
subtitle: The one about simple form lessons
categories: ruby rails simple_form
---
So I've messed with [simple_form](https://github.com/plataformatec/simple_form), another great project from [José Valim](https://github.com/josevalim).

I've gathered some of my lessons learned in this post. First of all I'm skipping the basics, since that's covered just fine in the [README](https://github.com/plataformatec/simple_form).

## Notes On Configuration

Remember to flip your rails server, when you do configuration changes. They will not be loaded on the fly in development.

## Wrappers

Wrappers was one of the things I had to dig in to, before figuring out how they work. The documentation explains how to set them up, but not really how they work.

So a wrapper is a configuration set that tells simple_form, how to render the components your form use. But what does that mean?

Let's look at a simple wrapper, looking something like this:

```ruby
config.wrappers :simple, tag: :div, error_class: :field_error, class: :form_field do |b|
  b.use :html5
  b.use :label
  b.use :input
  b.use :hint,  wrap_with: { tag: :span, class: :hint }
  b.use :error, wrap_with: { tag: :span, class: :error }
end
```

When you use this wrapper in a form, like this

```erb
# Here the wrapper is applied to all of the elements of the form
<%= simple_form_for @profile, wrapper: :simple do |f| %>
  <%= f.input :first_name %>
<% end %>

# Here it is only applied to the single field
<%= simple_form_for @profile do |f| %>
  <%= f.input :first_name, wrapper: :simple %>
<% end %>
```

Yes yes, but what does it do? Well ... It wraps. Our ```first_name``` input field friend from above, will be wrapped, like this

```html
<div class="form_field string required profile_first_name">
  <label class="string required control-label" for="profile_first_name">
    First name<abbr title="required">*</abbr>
  </label>
  <input class="string required" id="profile_first_name" name="profile[first_name]" size="50" type="text">
</div>
```

So there's a lot going on, and simple_form is indeed a powerful ally in maintaning forms across an application.

You can even nest the wrappers.

## Custom input

Custom input types goes into the ``` app/inputs ``` folder. They will be loaded by simple_form.

Let's take a look at a simple example. I want to add a weight type, thus appending the text ``` kg ``` to the input field.

It is as simple as this

```ruby
class WeightInput < SimpleForm::Inputs::NumericInput
  def input
    out = ''
    out << super # Render what the super class has to offer
    out << template.content_tag(:span, I18n.t('simple_form.units.defaults.kg'))
    out.html_safe
  end
end
```

You can build your output, prepending, appending and pretty much do what you like with the fields.

The above turns into this

```html
<input class="numeric weight optional" type="number" name="..."><span>Kg</span>
```

More to come...
