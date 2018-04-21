# Sage 9 friendly page walker

Sets up an alternate page walker for Sage 9-based themes.

To install, run the following in your Sage9-based theme directory:
```bash
composer require "MrDean/sage-pagewalker"
```

Include the pagewalker in your `wp_list_pages` function:

## As a [Controller](https://github.com/soberwp/controller) method (Recommended)
In your Controller, probably `app.php`
```php
/**
    * Subpage walker menu customization
    * @return array
    */
    public function walkersubmap() {
      $args = array(
        'title_li'          => '',
        //'child_of'          => $post->ID,
        'echo'              => 0,
        'walker'            => new Walker_Submap()
      );
      return $args;
    }
```

In your Blade file, probably `header.blade.php`
```php

  {!! wp_list_pages($pwalkersubmap) !!}

```

## Without Controller
If you're not setting up your template data with Controller, you'll need to fully reference the `\App\wp_bootstrap4_navwalker()`.
In your Blade file, probably `header.blade.php`
```php
@if (has_nav_menu('primary_navigation'))
  {!! wp_list_pages(['walker' => new \App\walkersubmap()]) !!}
@endif
```
