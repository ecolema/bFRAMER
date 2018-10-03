# TWIG Macros #
The theme contains two macro files: `html.twig` and `theme.twig`.

## HTML macros ##
Render HTML elements

### html.stylesheet ###
Link a stylesheet

```twig
{% macro stylesheet(url, async) %}
    <link rel="{{ async ? 'preload' : 'stylesheet' }}" href="{{ url }}"{% if async %} as="style" onload="this.rel='stylesheet'"{% endif %}>
{% endmacro %}
```

argument | description
--- | ---
`url` | absolute stylesheet path.
`async`(optional) | setting as `true` will prevent render blocking. This can only be used when called from within `<head>`

**usage:**
```twig
{{ html.stylesheet('//cdn.jsdelivr.net/npm/foundation-sites@6.3.0/dist/css/foundation.min.css') }}
```

### html.script ###
Define a client-side script

```twig
{% macro script(url, attribute) %}
    <script src="{{ url }}"{{ attribute ? ' ' ~ attribute : '' }}></script>
{% endmacro %}
```
argument | description
--- | ---
`url` | absolute script path
`attribute` (optional) | `defer \| async` run asynchronously (as soon as it is available) or run after the page has loaded

**usage:**
```twig
{{ html.script('//cdnjs.cloudflare.com/ajax/libs/jquery/3.3.1/jquery.js') }}
```

### html.textarea ###
Render a text `<input>`

```twig
{% macro input(name, value, class, placeholder, type, extra) %}
	<input type="{{ type|default('text') }}"{% if name %} name="{{ name }}"{% endif %}{% if value %} value="{{ value }}"{% endif %}{% if class %} class="{{ class }}"{% endif %}{% if placeholder %} placeholder="{{ placeholder }}"{% endif %}{% if extra %} {{ extra|raw }}{% endif %}>
{% endmacro %}
```
argument | description
--- | ---
`name` | create/populate `name=""` attribute as string
`value` | create/populate `value=""` attribute as string
`class` | create/populate `class=""` attribute as string
`placeholder` | create/populate `placeholder=""` attribute as string
`type` | populates `type=""` attribute. Default is `text`
`extra` | pass in raw HTML

**usage:**
```twig
{{ html.input('email', form_field_value('email', global.customer.email), 'required jsv_email', '','email', 'autocomplete="off"') }}
```

### html.button ###
Render a `<button>`

```twig
{% macro button(name, value, text, class, include_honeypot, type, icon, extra) %}
	{% if include_honeypot %}
		{{ _self.input(global.honeypot_field_name, '', 'hide', '', 'text', 'autocomplete="off"') }}
	{% endif %}
	<button type="{{ type|default('submit') }}"{% if name %} name="{{ name }}"{% endif %}{% if value %} value="{{ value }}"{% endif %}{% if class %} class="{{ class }}"{% endif %}{% if extra %} {{ extra|raw }}{% endif %}>
		{% if icon %}
            <i class="sw-icon-{{ icon }}" aria-hidden="true"></i>&nbsp;
        {% endif %}
        {{ text }}
	</button>
{% endmacro %}
```
argument | description
--- | ---
`name` | bar
`value` | value
`text` | text
`class` | class
`include_honeypot` | honeypot
`type` | type
`icon` | icon
`extra` | extra

**usage:**
```
{{ html.button('', '', 'Subscribe me', 'button', true) }}
```

### html.select ###
Render a `<select>`

```twig
{% macro select(name, values, selected, class, first_option, extra) %}
    <select{% if name %} name="{{ name }}"{% endif %}{% if class %} class="{{ class }}"{% endif %}{% if extra %} {{ extra|raw }}{% endif %}>
        {% if first_option %}
            <option value="">{{ first_option }}</option>
        {% endif %}
        {% for value in values %}
            <option value="{{ value.id|default(value) }}"{% if value.id|default(value) == selected %} selected="selected"{% endif %}>{{ value.name|default(value) }}</option>
        {% endfor %}
    </select>
{% endmacro %}
```
argument | description
--- | ---
`name` | name
`value` | value
`selected` | selected
`class` | class
`first_option` | first option
`extra` | extra

**usage:**
```twig
{{ html.select('country_id', countries, form_field_value('country_id', global.customer.country_id|default(222)), 'form-control medium custom-select', 'Select...') }}
```

### html.number_toggle ###
What does the macro do?

```twig
{% macro %}

{% endmacro %}
```
argument | description
--- | ---
`foo` | bar

**usage:**
```twig
{{ html.script }}
```

### html.image ###
What does the macro do?

```twig
{% macro %}

{% endmacro %}
```
argument | description
--- | ---
`foo` | bar

**usage:**
```twig
{{ html.script }}
```
### html.recursive_category ###
What does the macro do?

```twig
{% macro %}

{% endmacro %}
```
argument | description
--- | ---
`foo` | bar

**usage:**
```twig
{{ html.script }}
```

## Theme macros ##
Render theme specific blocks of code

### theme.text_snippet ###
What does the macro do?

```twig
{% macro %}

{% endmacro %}
```
argument | description
--- | ---
`foo` | bar

**usage:**
```twig
{{ html.script }}
```

### theme.sw_icon ###
What does the macro do?

```twig
{% macro %}

{% endmacro %}
```
argument | description
--- | ---
`foo` | bar

**usage:**
```twig
{{ html.script }}
```

### theme.link_list ###
What does the macro do?

```twig
{% macro %}

{% endmacro %}
```
argument | description
--- | ---
`foo` | bar

**usage:**
```twig
{{ html.script }}
```

### theme.errors ###
What does the macro do?

```twig
{% macro %}

{% endmacro %}
```
argument | description
--- | ---
`foo` | bar

**usage:**
```twig
{{ html.script }}
```

### theme.checkout_form_field ###
What does the macro do?

```twig
{% macro %}

{% endmacro %}
```
argument | description
--- | ---
`foo` | bar

**usage:**
```twig
{{ html.script }}
```

### theme.form ###
What does the macro do?

```twig
{% macro %}

{% endmacro %}
```
argument | description
--- | ---
`foo` | bar

**usage:**
```twig
{{ html.script }}
```

### theme.info_message ###
What does the macro do?

```twig
{% macro %}

{% endmacro %}
```
argument | description
--- | ---
`foo` | bar

**usage:**
```twig
{{ html.script }}
```

### theme.custom_form ###
What does the macro do?

```twig
{% macro %}

{% endmacro %}
```
argument | description
--- | ---
`foo` | bar

**usage:**
```twig
{{ html.script }}
```

### theme.honeypot ###
What does the macro do?

```twig
{% macro %}

{% endmacro %}
```
argument | description
--- | ---
`foo` | bar

**usage:**
```twig
{{ html.script }}
```

### theme.share_buttons ###
What does the macro do?

```twig
{% macro %}

{% endmacro %}
```
argument | description
--- | ---
`foo` | bar

**usage:**
```twig
{{ html.script }}
```

### macro.name ###
What does the macro do?

```twig
{% macro %}

{% endmacro %}
```
argument | description
--- | ---
`foo` | bar

**usage:**
```twig
{{ html.script }}
```
