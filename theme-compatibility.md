## Theme Compatibility - FluentCommunity

### Overview

FluentCommunity app runs on it's own template where it does not load WordPress resources for better performance and reduce conflicts. But you can still use the FluentCommunity Frame UI to your pages, posts or any custom post types.

### Using Block Themes
If you are using a block theme, You can use the default Block Based template provided by FluentCommunity for your page or posts. For other post types, or archives you can use FluentCommunity Page Layout Block to create a custom layout.

### Using Classic Themes
If you are using a classic theme, you can use the default template provided by FluentCommunity for your pages only. Currently, almost all the popular classic themes and page builders are compatible with FluentCommunity. If it does not work, please open a sppport ticket so we can investigate the issue.

Please check the documentation for [the official detailed guide](https://fluentcommunity.co/docs/theme-compatibility-feature/) for the Theme Compatibility Feature.

### Using Code Snippets
If you want to load FluentCommunity Page Layout Frame UI in your page / post / custom post types, you can use the PHP Code Snippets below:

```php
/**
*
* Use any of the following snippets depends on your need.
* You may target any specific post type or page type to load the fluent-community-frame.php
**/


// load fluent community frame only for single blog post
add_filter('fluent_community/template_slug', function ($templateSlug) {
    if(is_singular(['post'])) {
        return 'fluent-community-frame.php';
    }
    return $templateSlug;
});

// load fluent community frame only for post, blog index, category or taxonmy and author pages
add_filter('fluent_community/template_slug', function ($templateSlug) {
    if(is_singular(['post']) || is_home() || is_category() || is_tag() || is_author()) {
        return 'fluent-community-frame.php';
    }
    return $templateSlug;
});

// load fluent community frame for all the pages including posts, archives etc
add_filter('fluent_community/template_slug', function ($templateSlug) {
    return 'fluent-community-frame.php';
}, 10, 2);
```
