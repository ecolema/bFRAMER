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
`name` | create/populate `name=""` attribute as string
`value` | create/populate `value=""` attribute as string
`text` | button text
`class` | create/populate `class=""` attribute as string
`include_honeypot` | see `html.honeypot`
`type` | populates `type=""` attribute. Default is `submit`
`icon` | see `theme.icon`
`extra` | pass in raw HTML

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
`name` | create/populate `name=""` attribute as string
`values` | array of values to render as `<option value="">`
`selected` | marks matched `option` value as `selected`
`class` | create/populate `class=""` attribute as string
`first_option` | creates a valueless option as string. e.g. `'please select..'` 
`extra` | pass in raw HTML

**usage:**
```twig
{{ html.select('country_id', countries, form_field_value('country_id', global.customer.country_id|default(222)), 'form-control medium custom-select', 'Select...') }}
```

### html.number_toggle ###
Render a number toggle field

```twig
{% macro number_toggle(name, value, class, placeholder, type, extra, minus_text, plus_text) %}
    <div class="number-toggle">
        <button class="toggle-down">{{ minus_text|default('-') }}</button>
        <input type="{{ type|default('text') }}"{% if name %} name="{{ name }}"{% endif %}{% if value %} value="{{ value }}"{% endif %}{% if class %} class="{{ class }}"{% endif %}{% if placeholder %} placeholder="{{ placeholder }}"{% endif %}{% if extra %} {{ extra|raw }}{% endif %}>
        <button class="toggle-up">{{ plus_text|default('+') }}</button>
    </div>
{% endmacro %}
```
argument | description
--- | ---
`name` | create/populate `name=""` attribute as string
`value` | create/populate `value=""` attribute as string
`class` | create/populate `class=""` attribute as string
`placeholder` | create/populate `placeholder=""` attribute as string
`type` | create/populate `type=""` attribute as string. Default is `text
`extra` | pass in raw HTML
`minus_text` | string. Default is `'-'`
`plus_text` | string. Default is `'+'`

**usage:**
```twig
{{ html.script }}
```

### html.image ###
Render an `<img>`

```twig
{% macro image(src, alt, class, extra, lazy, no_image) %}
    {% set image_src = src ? src : no_image ? asset_url('images/no_image.png') : src %}
    {% set loader = asset_url('images/loading.gif') %}
    {% if lazy %}
        <img src="{{ loader }}" data-src="{{ image_src }}" alt="{{ alt }}"{% if class %} class="{{ class }}{{ lazy ? ' lazy' : '' }}"{% endif %}{% if extra %} {{ extra|raw }}{% endif %}>
    {% else %}
        <img src="{{ image_src }}" alt="{{ alt }}"{% if class %} class="{{ class }}"{% endif %}{% if extra %} {{ extra|raw }}{% endif %}>
    {% endif %}
{% endmacro %}
```
argument | description
--- | ---
`src` | populatea `src=""` attribute as string
`alt` | populates `alt=""` attribute as string
`class` | create/populate `class=""` attribute as string (optional)
`extra` | pass in raw HTML
`lazy` | set as `true` to lazy load the image (optional)
`no_image` | set as `true` to render a custom image if `src` fails to return an image

**usage:**
```twig
{{ html.image(photo_url, item.photo_description, 'item-img', '', '', true) }}
```
### html.recursive_category ###
Renders a multi level caetgory list

```twig
{% macro recursive_category(catID, level, limit) %}
    {% set catparent = category(catID) %}
    {% if limit == 0 or limit > level %}
        <li{% if catparent.categories %} class="has-child"{% endif %}>
            <a href="{{ catparent.url }}">{{ catparent.title }}</a>
            {% if catparent.categories|length %}
                <ul class="submenu level-{{ level|default(1) }}">
                    {% for category in catparent.categories %}
                        {{ _self.recursiveCategory(category.id, level > 0 ? level + 1 : 2) }}
                    {% endfor %}
                </ul>
            {% endif %}
        </li>
    {% endif %}
{% endmacro %}
```
argument | description
--- | ---
`catID` | Source category ID
`level` | integer to signal start level (optional) 
`limit` | integer for how many sub levels to output. Set as `0` for no limit.

**usage:**
```twig
{% set root_cat = 40468 %}
{{ theme.recursive_category(root_cat, '', '')
```

## Theme macros ##
Render theme specific blocks of code

### theme.text_snippet ###
Renders a text snippet

```twig
{% macro text_snippet(name, raw) %}
    {% if raw %}
		{{ global.theme.settings['text_' ~ name] }}
    {% else %}
        {{ global.theme.settings['text_' ~ name]|raw }}
    {% endif %}
{% endmacro %}
```
argument | description
--- | ---
`name` | bar
`raw` | bar

**usage:**
```twig
{{ theme.text_snippet('empty_basket') }}
```

### theme.sw_icon ###
Render a font Icon glyph

```twig
{% macro sw_icon(name, text) %}
    <i class="sw-icon-{{ name }}" aria-hidden="true"></i>
    {% if text %}
        <span class="show-for-sr">{{ text }}</span>
    {% endif %}
{% endmacro %}
```
argument | description
--- | ---
`name` | bar
`text` | bar

**usage:**
```twig
{{ theme.sw_icon('gift') }}
```

### theme.link_list ###
What does the macro do?

```twig
{% macro link_list(name, class, include_title) %}
	{% set link_list = global.theme.settings['list_' ~ name] %}
	{% if link_list and link_list.links %}
		{% if include_title and link_list.title %}
			<h4>
				{{ link_list.title }}
			</h4>
		{% endif %}
		<ul class="{{ class }}">
			{% for link in link_list.links %}
				<li>
					<a href="{{ link.url }}">
						{{ link.title }}
					</a>
				</li>
			{% endfor %}
		</ul>
	{% endif %}
{% endmacro %}
```
argument | description
--- | ---
`name` | bar
`class` | bar
`include_title` | bar

**usage:**
```twig
{{ theme.link_list('footer', 'footer-list menu vertical medium-horizontal', 0) }}
```

### theme.errors ###
Renders an list of platform errors

```twig
{% macro errors(errors) %}
	{% if errors %}
		<div class="{{ class|default('shopwired-info-message') }}" role="alert">
			{% for error in errors %}
				{% if not loop.first %}
					<br>
				{% endif %}
				{{ error }}.
			{% endfor %}
		</div>
	{% endif %}
{% endmacro %}
```
argument | description
--- | ---
`errors` | bar

**usage:**
```twig
{{ theme.errors(errors) }}
```

### theme.checkout_form_field ###
Render a checkout form field 

```twig
{% macro checkout_form_field(name, field, labels, small, shipVal) %}
    {% set required_array = global.theme.settings.checkout_phone_required ? ['phone'] : [] %}
	<label class="checkout-field checkout-field-{{ name }} column large-{{ small ? '6' : '12' }}">
        {% set label = labels|default(name|title) %}
        {% set value = field.value|default(shipVal) %}
        <span class="field-label">{{ label }}</span>
		{% if field.readonly %}
			<input type="text" value="{{ value }}" data-name="{{ name }}" readonly>
		{% elseif field.options is defined %}
			<select name="{{ field.name }}" data-name="{{ name }}"{% if field.required or name in required_array %} class="required"{% endif %}>
				<option value="">Please select...</option>
				{% for option in field.options %}
					<option value="{{ option.id|default(option) }}"{% if option.id|default(option) == value %} selected="selected"{% endif %}>
						{{ option.name|default(option) }}
					</option>
				{% endfor %}
			</select>
		{% else %}
			<input type="text" name="{{ field.name }}" value="{{ value }}" data-name="{{ name }}"{% if field.required  or name in required_array %} class="required"{% endif %}>
		{% endif %}
	</label>
{% endmacro %}
```
argument | description
--- | ---
`name` | bar
`field` | bar
`labels` | bar
`small` | bar
`shipVal` | bar

**usage:**
```twig
{# Render billing fields #}
{% for name, label in labels %}
	{% set field = checkout.billing[name] %}
	{% set shipVal = checkout.shipping[name].value %}
	{% set size = name in small ? 1 : 0 %}
	{{ theme.checkout_form_field(name, field, label, size, shipVal) }}
{% endfor %}
```

### theme.form ###
What does the macro do?

```twig
{% macro form(fields, errors, labels, button_text, is_account_form) %}
	{{ _self.errors(errors) }}
	<form action="{{ global.current_url }}" method="post" class="form-with-validation">
		{% for name, field in fields %}
			{% set label = labels[name]|default(name|title) %}
			{% set type = field.type|default('text') %}

            {% if type == 'boolean' %}
                <div class="row column">
                    <input id="{{ field.name }}" type="checkbox" name="{{ field.name }}">
                    <label for="{{ field.name }}">{{ label }}</label>
                </div>
            {% else %}
    			<label>
    				<span class="field-label">{{ label }}</span>
    				{% if field.values is defined %}
    					<select name="{{ field.name }}"{% if field.required %} class="required"{% endif %}>
    						{% if name == 'source' or name == 'rating' %}
    							<option value="">Please select...</option>
    						{% endif %}
    						{% for value, label in field.values %}
    							<option value="{{ value }}"{% if value == field.value %} selected="selected"{% endif %}>
    								{{ label }}
    							</option>
    						{% endfor %}
    					</select>
    				{% elseif type == 'boolean' %}
    					<br>
    					<input type="checkbox" name="{{ field.name }}" value="1"{% if field.value %} checked="checked"{% endif %}>
    				{% elseif type == 'hidden' %}
    					<input type="hidden" name="{{ field.name }}" value="{{ field.value }}">
    					{% if name == 'amount' %}
    						<br>
    						{{ format_price(field.value) }}
    					{% endif %}
    				{% elseif name == 'message' or name == 'content' %}
    					<textarea name="{{ field.name }}" cols="30" rows="3"{% if field.required %} class="required"{% endif %}>{{ field.value }}</textarea>
    				{% else %}
    					<input type="text" name="{{ field.name }}" value="{{ field.value }}"{% if field.required %} class="required"{% endif %}{% if is_account_form and (name == 'email_address' or type == 'password') %} autocomplete="off"{% endif %}>
    				{% endif %}
    			</label>
            {% endif %}
		{% endfor %}
		<input type="text" name="{{ global.honeypot_field_name }}" class="hide" autocomplete="off">
		<button type="submit" class="button">
			{{ button_text|default('Submit') }}
		</button>
	</form>
{% endmacro %}
```
argument | description
--- | ---
`fields` | bar
`errors` | bar
`labels` | bar
`button_text` | bar
`is_account_form` | bar

**usage:**
```twig
{# Render account form #}
{{ theme.form(form_fields, errors, labels, button_text, true) }}
```

### theme.info_message ###
Renders platform information message `global.info_message`.

```twig
{% macro info_message(class) %}
    {% if global.info_message %}
        <div class="{{ class|default('shopwired-info-message') }}">
            {{ global.info_message|raw }}
        </div>
    {% endif %}
{% endmacro %}
```
argument | description
--- | ---
`class` | className, default is `.shopwired-info-message`

**usage:**
```twig
{{ theme.info_message(errors) }}
```

### theme.custom_form ###
Render a form which submits to a specified email address.

```twig
{% macro custom_form(settings) %}
    <input type="hidden" name="custom_form" value="1">
    {% for name, value in settings %}
        <input type="hidden" name="custom_form_{{ name }}" value="{{ value }}">
    {% endfor %}
{% endmacro %}
```
argument | description
--- | ---
`settings` | array of hidden fields

**usage:**
```twig
{{ shopwired.custom_form({ 
    'to_email': 'info@joesshoeshop.com', 
    'from_email': 'info@joesshoeshop.com', 
    'redirect_url': '/thanks', 
    'subject': 'new website enquiry' 
}) }}
```

### theme.honeypot ###
What does the macro do?
Adds an invisible field to your form (that only spambots can see) to trick them into revealing that they're spambots and not actual end-users.

```twig
{% macro honeypot(class) %}
    <input type="text" name="{{ global.honeypot_field_name }}" autocomplete="off" class="{{ class|default('shopwired-form-field') }}">
{% endmacro %}
```
argument | description
--- | ---
`class` | ClassName, default is `.shopwired-form-field`

**usage:**
```twig
{{ theme.honeypot('hide') }}
```

### theme.share_buttons ###
Render social media share buttons

```twig
{% macro share_buttons(url, title, description, photo, icon, class) %}
    <ul class="{{ class|default('menu simple') }}">
        <li>
            <a href="https://www.facebook.com/sharer/sharer.php?u={{ url|url_encode }}&t={{ title|url_encode }}"
               class="facebook"
               target="_blank">
               {% if icon %}
                   {{ _self.fa('facebook') }}
               {% endif %}
               <span class="{{ icon ? 'show-for-sr' : 'inner' }}">
                   Share on Facebook
               </span>
            </a>
        </li>
        <li>
            <a href="https://twitter.com/home/?status={{ (title ~ ' (' ~ url ~ ')')|url_encode }}"
               class="twitter"
               target="_blank">
               {% if icon %}
                   {{ _self.fa('twitter') }}
               {% endif %}
                <span class="{{ icon ? 'show-for-sr' : 'inner' }}">
                    Share on Twitter
                </span>
            </a>
        </li>
        <li>
            <a href="https://pinterest.com/pin/create/button/?url={{ url|url_encode }}&media={{ photo|url_encode }}&description={{ description|striptags|slice(0, 500)|trim|url_encode }}"
               class="pinterest"
               target="_blank">
               {% if icon %}
                   {{ _self.fa('pinterest') }}
               {% endif %}
               <span class="{{ icon ? 'show-for-sr' : 'inner' }}">
                   Pin It
               </span>
            </a>
        </li>
        <li>
            <a href="https://plus.google.com/share?url={{ url|url_encode }}"
               class="google"
               target="_blank">
               {% if icon %}
                   {{ _self.fa('google-plus') }}
               {% endif %}
               <span class="{{ icon ? 'show-for-sr' : 'inner' }}">
                   Share on Google+
               </span>
            </a>
        </li>
        <li>
            <a href="http://www.tumblr.com/share/link?url={{ url|url_encode }}&name={{ title|url_encode }}"
               class="tumblr"
               target="_blank">
               {% if icon %}
                   {{ _self.fa('tumblr') }}
               {% endif %}
               <span class="{{ icon ? 'show-for-sr' : 'inner' }}">
                   Share on Tumblr
               </span>
            </a>
        </li>
    </ul>
{% endmacro %}
```
argument | description
--- | ---
`url` | absolute URL of shared content
`title` | title of shared content
`description` | optional description
`photo` | absolute URL of shared content media
`icon` | boolean to indicate if font icons should be rendered.
`class` | className for parent `ul`

**usage:**
```twig
{{ theme.share_buttons(global.current_url, post.title, post.content, post.thumbnail.image_url, true, 'social-menu menu simple') }}
```
