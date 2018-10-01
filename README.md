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
For headings, paragraphs, links, horizontal rules and anything typographical. Elements in this section are styled in `/assets/scss/_typography.scss`.

### Icons ###
'Icons' are the exception. Standard font icons appear here. Additional icons can be added to the icon font. Do not code them as `<img>` elements or CSS `background-image`.

#### Extend Icon Font ####
Visit [IcoMoon](https://icomoon.io/app/), click 'import icons' and upload `/assets/fonts/sw-icons.json`.

Add new icon gylphs as reqired and generate a new font set.

Please replace the following theme files with those generated in the new icon set:
* `/assets/fonts/sw-icons.svg`
* `/assets/fonts/sw-icons.ttf`
* `/assets/fonts/sw-icons.woff`
* `/assets/fonts/sw-icons.json`

Replace the icons CSS in `/assets/scss/_fonts.scss` found under `// icons `.

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
Elements in this section are styled in `/assets/scss/_forms.scss`.

### Form components ###
Textual form elements adopt the following structure for increased accessibility:
```html
<label>
    <span class="field-label">Input Label</span>
    <input type="text">
</label>
````
> Please note the `<label>` element is used as a container. Label text is selected with the className `.field-label`.

#### Validation errors ####
Form validation error mesaages will appear after the label text `<span class="field-label"></span>`.

The className `.validation-error` is applied to the input and error message itself. To differentuial, the selector for the message text only is `span.validation-error`.

#### Checkbox and Radio Elements ####
Default styling for checkbox and radio buttons are customised with a CSS only solution. Both are controled in `_forms.scss`.

Modal | CSS selector
--- | ---
Age Verification | `.verify-age-modal`
newsletter | `.newsletter-modal`

### Contact Form ###
The contact form consists of form components and typically appears on the `/contact-us` page.

Please add custom styles for the product form in `/assets/scss/_forms.scss` too.

## Components ##
For specific UI components. This is where majority of theme styles are placed. UI components are often composed of Objects and Components.

Elements in this section are styled in SCSS component files: `/assets/scss/_components*.scss`. Unless specified, styles should be placed in `/assets/scss/_components.scss`

### Announcement Bar ###
Closable message block that appears above the site header.

### Home page banner carousel ###
Displays an array of gallery images in a collection displayed as an image carousel using [slick](http://kenwheeler.github.io/slick/).

Becuase image slides on mobile phone displays ofter require seperate art direction, the banners are split into `large` and `small`. By default `gallery_home_mobile` banners are displayed for the `small` breakpoint only.

### Generic carousel ###
Generic image slider styles include positioning and display of previous/next arrows for all elements which use the slick slider plugin.

Examples of generic sliders include Home page 'featured products' and product page 'related products'.

The className `.product-slider` is used to display a collection as a slider.

### Product thumbnails ###
styled in `/assets/scss/_components_product.scss`.

### Star raiting ###
Combines a twig `for` loop with the macro `sw_icon` to output star icons to represent a raiting.

### Product labels ###
Product labels denote whether a product is 'new' or included in a volume discount such as '3 for 2' or '2 for 1'.

Combined [Foundation's label element](https://foundation.zurb.com/sites/docs/label.html) with the following classes:
* `.two-for-one`
* `.three-for-two`
* `.new`

### Modal dialogs ###
Modal dialogs use [Foundation's Reveal component](https://foundation.zurb.com/sites/docs/reveal.html).

The theme includes 2 default modals. The markup can be modified in `/views/partials/global_modals.twig`:

### Off canvas basket ###
The off canvas basket is styled in `/assets/scss/_components_basket_offcanvas.scss`.

`offCanvasBasket` uses [Foundation's Off-canvas component](https://foundation.zurb.com/sites/docs/off-canvas.html).

### Basket item ###
styled in `/assets/scss/_components_basket.scss`.

A basket item represents a table row of `basket-table`, displayed on  the `/checkout/basket` view.

### Basket totals ###
styled in `/assets/scss/_components_basket.scss`.

The table `basket-totals` appears on the the `/checkout/basket` view and displays totals related to the items in `basket-table`.

### Basket rewards ###
styled in `/assets/scss/_components_basket.scss`.

`.basket-info-rewards` is displayed in 3 different states:
* 'Can convert' - points can be redeeemed against basket items
* 'Converted' - points have been redeemed aginst basket items
* 'Cannot convert - points will be earned against basket items but cannot be converted

### Delivery rate radio buttons ###
styled in `/assets/scss/_components_basket.scss`.

Specific styling for delivery rates where the theme setting 'Delivery rate radio buttons' is enabled.

### Basket voucher ###
styled in `/assets/scss/_components_basket.scss`.

Using [Foundation's Toggler component](https://foundation.zurb.com/sites/docs/toggler.html) to toggle the basket voucher form.

### Currency dropdown ###
Displayed in the site header, used for selecting a currency and shipping region.

Uses [Foundation's Dropdown componenet](https://foundation.zurb.com/sites/docs/dropdown.html).

The flag images are displayed using a sprite sheet `/assets/images/flags[size].png`. By default flag images are displayed with `flags32.png` (where each flag is 32 x 32 pixels).

Render 16 x 16 flag images by altering `$flags-size` in `/assets/scss/_flags.scss`. 

### Account dropdown ###
Links are displayed reletive to the user's logged in status. 

Uses [Foundation's Dropdown componenet](https://foundation.zurb.com/sites/docs/dropdown.html).

### Footer link lists ###
styled in `/assets/scss/_components_footer.scss`.

Links lists are rendered with the macro `link_list`. 

### Footer newsletter ###
Styled in `/assets/scss/_components_footer.scss`.

### Company contact information ###
Renders basic company contact information, displayed in the contact view (/contact-us).

### Catgeory Menu ###
Renders a responsive caetory menu using [Foundation's Responsive Menu](https://foundation.zurb.com/sites/docs/responsive-navigation.html#responsive-menu).

### Breadcrumb ###
Uses [Foundation's Breadcrumbs component](https://foundation.zurb.com/sites/docs/breadcrumbs.html).

### Pagination ###
Uses [Foundation's Pagination component](https://foundation.zurb.com/sites/docs/pagination.html).

### Sidebar menus ###
Uses [Foundation's Accordion Menu component](https://foundation.zurb.com/sites/docs/accordion-menu.html), side bar menus are navigation elements displayed in a side bar column.

Sidebar menus include:
* Sidebar category menu - for categories
* Content pages menu - Rending page links stored in the sidebar links list `list_sidebar`
* Filter menu - Uses [Foundation's Accordion component](https://foundation.zurb.com/sites/docs/accordion.html) to display filter groups
* Blog category/archive menus - for blog navigation

### Collection sort form ###

### Product page prices ###
styled in `/assets/scss/_components_product.scss`.

### Variant buttons ###
styled in `/assets/scss/_components_product.scss`.

### Product buy buttons ###
styled in `/assets/scss/_components_product.scss`.

### Product page info ###
styled in `/assets/scss/_components_product.scss`.

### Product description tabs ###
styled in `/assets/scss/_components_product.scss`.

### Product tiles ###

### Category tiles ###

### Article tiles ###

### Recent product tiles ###

### Video tiles ###

### Gallery tiles ###

### Gallery image tiles ###

### Stockiest tiles ###









