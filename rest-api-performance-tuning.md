## REST API performance Tuning
FluentCommunity is built for performance and normally you don't need any extra configaration for performance tuning. We highly recommend to use Redis Object Caching (You don't need the Pro version of Object Caching). 

If you are using FluentCommunity with lots of heavy plugis, Other plugins may slow down the REST API responses as it's loads and do lots of Database queries even they don't need to. In this guide, you can explicitly enable which plugins will be loaded on FluentCRM REST API requests. This will help you to speed up the REST API requests and reduce the load on your server.

> [!WARNING]  
> **This is an advanced feature and should only be used by developers.**

### How It works
This snippet will check if it's a FluentCommunity REST API calls or not not and then it will load only the defined plugins and offload the rest of the plugins. This will help you to speed up the REST API requests and reduce the load on your server.

### How to use it

1. create a file at `/wp-content/mu-plugins/fluent-api-performance-tuning.php`
2. Copy the code below and paste it in the file
3. Test your FluentCommunity Portal and see if everything is working fine


```php
<?php defined('ABSPATH') || exit;
/**
 * Plugin Name: FluentCommunity Express REST API
 * Description: An MU Plugin for FluentCommuynity to load only the required plugins for the REST API. If you have lots of plugins installed and activated, this plugin will help you to load only the required plugins for the REST API and increase the REST API performance.
 * Version: 1.0
 * Author: Shahjahan Jewel
 * Author URI: https://fluentcommunity.co
 * Plugin URI: https://github.com/WPManageNinja/fluent-community-docs/blob/master/rest-api-performance-tuning.md
 */

add_filter('option_active_plugins', function ($plugins) {
    $requestUrl = isset($_SERVER['REQUEST_URI']) ? $_SERVER['REQUEST_URI'] : '';
    if (strpos($requestUrl, 'wp-json/fluent-community/v2') === false) {
        return $plugins;
    }

    // $plugins to load (when available)
    $pluginsToLoad = [
        'fluent-community/fluent-community.php', // for fluent community
        'fluent-community-pro/fluent-community-pro.php', // for fluent community pro
        'fluent-smtp/fluent-smtp.php', // for sending emails
        'fluent-crm/fluent-crm.php', // FluentCRM Integration
        'fluentcampaign-pro/fluentcampaign-pro.php', // FluentCRM Pro Integration
        'easy-code-manager/easy-code-manager.php', // fluent snippets
        // add more plugins here as needed
    ];

    $plugins = array_intersect($plugins, $pluginsToLoad);
    $plugins = array_values($plugins);

    return $plugins;
});
```

### Important Notes
- This is an advanced feature and should only be used by developers.
- If you are not using lots of plugins, you don't need to use this feature.
- You must have to use it as a mu-plugins otherwise it won't work.


