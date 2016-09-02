---
title: Craft theme documentation

language_tabs:
  - php
  - scss
  - javascript
  - shell

toc_footers:
  - <a href='https://drivdigital.no'>A Driv Digital Product</a>

search: true
---

# Craft

Craft, formally Drivkraft, is an extension of the previous Driv Starter theme that we created.
It takes every lesson we learn while creating websites for clients and rebundles it into something that will aid future clients

## Starting with a child theme

```terminal
git clone git@github.com:drivdigital/craft-child.git
```

Because your child theme is going to be customised to suit your website, we cannot include the child as part of the composer install.
the easiest way to install the theme is to download the repo here: [https://github.com/drivdigital/craft-child](https://github.com/drivdigital/craft-child)

Another way of downloading the theme is to pull it into your themes directory.

<aside class="notice">
You must install the child theme, you must activate it to see your changes.
</aside>

## Grunt

```shell
# Install required dependencies
sudo npm install
# Run grunt to compile css
grunt
```

You need to run `npm install` or `sudo npm install` in the child theme folder to install the dependencies needed to complile.


# Content management

Using Adanced custom fields, Craft comes with a layout building method that utilised the Flexible Content field.

What this means is that most of your work is dont doe you when it comes to getting clients to build visually nice websites.

The current list of layouts available are:

## Paragraph

```php
  <div class="paragraph cf">
    <div class="paragraph--container w cf">
      <?php echo $paragraph; ?>
    </div>
  </div>
```
```scss
.paragraph{
  &--container{
    // Styling paragraphs
  }
}
```

A straight up replacement for `the_content`. This is just a regular wysiwyg and can have media within the content area.

## Image

Inserts an image into the flow of content. By default, the image will be constrained to the width of the wrapper. There is a `boolean` option for **Edge to edge** for extending past the wrapper.

<aside class="notice">
Edge to Edge will break the layout of the page and expand to the full width of the browser window. Do not use tall images here, or your site might be a lttle longer than you expected...
</aside>

## Banner

Banner gives the option to select banners created in the Banners Post type.
You have the option of selecting one of four layout options for the banners.

If the banner selection is `Single`, you're able to utilise the `Slider` option and show multiple slides.

You can learn more about banners in the banner section below

## Banner group

Banner groups are created though the Banner post type as a way of grouping banners that are often used together.

You can select which banner group to display here, rather than manually picking the banners

## Product list

When you chose product lists, you can display products in four different ways:

- Category selection
- Featured products
- Best sellers
- New products

## Columns of text

List columns of wysiwyg content

## Popular categories

List the categories that are popular with woocommerce

## Block

Reusable blocks

## Sub page list

```scss
// Target each page that displays
.parent-sub-page{
  // Target the container -pluralised
  &s{
    // Change the layout
  }
}
```

A more managable way to display child posts of the current page you're on, or show a list of posts in general.

Two `boolean` options are:

- Show thumbnails
- Show excerpts


# Banners

Craft comes with build in Banner management. This comes in the form of a menu item in the Dashboard called `Banners`

# Actions

Actions are ways of changing the content and functions of the site without being destructive. Here's a breakdown of our custom actions that you can edit in the child theme:

<aside class="notice">
To unhook Craft's parent features, you need to reference the class that is used. The classes can be found in the `classes` folder in the Craft Theme.
</aside>

## Header

> You're able to unhook actions and replace them with your own:

```php
<?php
  // This action removed the USPs from the top left of the header
  remove_action( 'drivkraft_header_top_left', 'drivkraft_header::header_usp_items' );

  // This action places the USPs to the right of the header
  add_action( 'drivkraft_header_top_right', 'drivkraft_header::header_usp_items'  )
```

By default, the head is split into three columns and two rows:

Left | Center | Right
-----|--------|------
USP List | Logo | Account menu
Search | Main Navigation | Cart

**Class:** `drivkraft_header`

- `drivkraft_header_top_left`
- `drivkraft_header_top_center`
- `drivkraft_header_logo`
- `drivkraft_header_top_right`
- `drivkraft_header_bottom_left`
- `drivkraft_header_search`
- `drivkraft_header_bottom_center`
- `drivkraft_header_bottom_right`




## Body
```php
<?php
// Add google tag manager script after the body
  add_action( 'drivkraft_after_body_tag', __CLASS__ . '::custom_google_script' );

  static function custom_google_script() {
    echo '<script>...</script>';
  }
```
### After body tags
Sometimes you need to insert google scripts, and against their own advice, they always tell you to load it after the opening body tag. You can hook a script into here by using this action

```php
<?php
  // Insert a sidebar before flexible layouts to display widgets
  add_action( 'drivkraft_before_flex_layout', __CLASS__ . '::sidebar_before_content' );

  static function sidebar_before_content() {
    get_sidebar();
  }
```
### Adding to the content area
You need to add to the content area, or around the area most often than not. You can use the following actions to modify the layout of the page.

- `drivkraft_before_flex_layout`
- `drivkraft_after_flex_layout`
- `drivkraft_before_front_content`
- `drivkraft_after_front_content`
- `drivkraft_before_page_content`
- `drivkraft_after_page_content`
- `drivkraft_before_flex_failed_layout`
- `drivkraft_after_flex_failed_layout`



## Header cart
- `drivkraft_before_empty_cart`
- `drivkraft_after_empty_cart`

```php
<?php
  // Showing a 'nobody came to my party' animation when the cart is empty
  add_action( 'drivkraft_empty_cart_message', __CLASS__ . '::empty_cart_billy_no_mates' );

  static function empty_cart_billy_no_mates(){
    echo '<svg...>';
  }
```

When your shopping cart is empty, you can display a custom message or products that you recommend:

- `drivkraft_empty_cart_message`

## Articles
- `drivkraft-time`
- `drivkaraft_archive_after`
- `drivkraft_archive_before`
- `drivkraft_archive_sidebar`
- `drivkraft_after_article_excerpt`
- `drivkraft_before_article_title`
- `drivkraft_after_article_title`
- `drivkraft_single_blog_before`
- `drivkraft_single_blog_after`

## Banners
- `drivkraft_banners_after_title`


## 404s and heartbeats

- `drivkraft_theme_before_404`
- `drivkraft_theme_404`
- `drivkraft_theme_after_404`

## Menus

- `account_additional_items`
- `mega_menu_additional_items`
- `mega_menu_page_item_children // Target page name`
- `mega_menu_page_item_class // Target page name`

## Woocommerce

- `drivkraft_single_product_after_title`
- `drivkraft_single_product_before_title`
- `drivkraft_single_product_after_title_price`
- `drivkraft_single_product_before_title_price`

### Categories
- `drivkraft__extended-filter`
- `drivkraft_maybe_pagination`


### Terms and Conditions
Currently, there are only two options available for the checkout page that we've created:

- `woocommerce_checkout_after_terms_and_conditions`
- `woocommerce_checkout_before_terms_and_conditions`



