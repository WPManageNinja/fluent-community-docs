# Useful Code Snippets for FluentCommunity Plugin

This documentation provides a collection of useful code snippets for developers working with the FluentCommunity Plugin or just customize the portal's default behavior. These snippets can help you customize and extend the functionality of the plugin to meet your specific needs. We recommend to use [FluentSnippet plugin](https://wordpress.org/plugins/easy-code-manager/) to manage these snippets.


### Modify Portal URL Slug<a name="portal_slug"></a>
By default the portal URL is `/portal`. You can change it to something else like `/community`.

```php
define('FLUENT_COMMUNITY_PORTAL_SLUG', 'community');
```
This code need to be placed in your wp-config.php file. After add this, make sure you resave the permalink settings to flush the rewrite rules.

### Add Custom CSS to Portal<a name="custom_css"></a>
You can add custom CSS to the portal by using the following code 

```php
add_action('fluent_community/portal_head', function() {
    ?>
    <style>
        /* Add your custom CSS here */
    </style>
    <?php
});
```

If you want to add your own CSS file, you can use the following code

```php
add_action('fluent_community/portal_head', function() {
    ?>
    <link rel="stylesheet" href="url_of_your_css_file" media="all">
    <?php
});
```

Similar to header hook you also have footer hook to add your custom javascript files: `fluent_community/portal_footer`
