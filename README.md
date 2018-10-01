# Style guide #
For code efficiency and UI consistency we use a living style guide. The living style guide provides a set of standards for the use and creation of styles.

In the case of a standard style guide, the purpose is to maintain brand cohesiveness and prevent the misuse of graphics and design elements. In the same way, a living stye guide is used to maintain code consistency and guide implementation.

The living style guide can be viewed by visiting `/styleguide`.

> We use Foundation v6.3 with the ['Float Grid'](https://foundation.zurb.com/sites/docs/grid.html). ’Flex’ and ‘XY’ grids are not used becuase they are not supported by Internet Explorer 9.

Style guide content is split into distinct sections.  

## Variables ##
Contains an overview of SCSS variables defined in `/assets/scss/_variables.scss`.
If new variables are created, please consider documenting usage in the style guide's 'variables' section.

## Typography ##
For headings, paragraphs, links, horizontal rules and anything typographical. Elements in this section should be styled in `/assets/scss/_typography.scss`.

'Icons' are the exception. 
Standard font icons appear here. The PSD may include additional icons. Please add additional icons to the icon font. Do not code them as `<img>` elements or CSS `background-image`.

To extend the icon font, visit [IcoMoon](https://icomoon.io/app/), click 'import icons' and upload `/assets/fonts/sw-icons.json`.

Please replace the following theme files with those generated in the new icon set:
* `/assets/fonts/sw-icons.svg`
* `/assets/fonts/sw-icons.ttf`
* `/assets/fonts/sw-icons.woff`
* `/assets/fonts/sw-icons.json`

And replace the icons CSS in `/assets/scss/_fonts.scss` found under `// icons `.

## Controls ##
For button elements. Please use the cascasde to style buttons, by overriding the default button styles in `/assets/scss/_controls.scss`.

In SCSS this may resemble the following:
```scss
.button {
    // default button
    
    &.secondary {
        // secondary button
    }
    
    // etc.
}
```

## Forms ##
Something about forms

### Form components ###

### Contact Form ###


## Components ##
Something about components

### Announcement Bar ###

### Homepage banner carousel ###

### Generic carousel ###

### Product thumbnails ###

### Star raiting ###

### Product labels ###

### Modal dialogs ###

### Off canvas basket ###

### Basket item ###

### Basket totals ###

### Basket rewards ###

### Delivery rate radio buttons ###

### Basket voucher ###

### Currency dropdown ###

### Account dropdown ###

### Footer link lists ###

### Footer newsletter ###

### Company contact information ###

### Catgeory Menu ###

### Breadcrumb ###

### Pagination ###

### Sidebar menus ###

### Collection sort form ###

### Sidebar menus ###

### Collection sort form ###

### Product page prices ###

### Variant buttons ###

### Product buy buttons ###

### Product page info ###

### Product description tabs ###

### Product tiles ###

### Category tiles ###

### Article tiles ###

### Recent product tiles ###

### Video tiles ###

### Gallery tiles ###

### Gallery image tiles ###

### Stockiest tiles ###









