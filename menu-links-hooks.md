## Add Custom Links to different Community Elements

You can add custom links to different community elements like the header, space menu, user profile etc.

### Add Custom Links to the Header (Right side icons)

```php

add_action('fluent_community/before_header_menu_items', function ($currentProfile) {
    if($currentProfile) {
        return; // we want to show this only for non-logged in users
    }
    ?>
        <li class="top_menu_item">
            <a href="https://example.com">
                <div class="chat_icon">
                    <i class="el-icon">
                        <!--SVG COde -->
                    </i>
                </div>
            </a>
        </li>
    <?php
});
```

### Add Custom Links to the Space Menu

```php
add_filter('fluent_community/space_header_links', function ($links, $space) {
    
    // $space->membership will be null if the user is not a member of the space
    
    $links[] = [
        'title' => 'Custom Link',
        'url' => 'https://example.com'
    ];
    return $links;
}, 10, 2);
```

### Add Custom Links User Profile Menu

```php

add_filter('fluent_community/profile_view_data', function ($data, $xprofile) {
    $data['profile_nav_actions'][] = [
        'css_class' => 'YOUR_CSS_CLASS',
        'title'     => 'custom link',
        'svg_icon'  => '<svg>...</svg>', // optional
        'url'       => 'https://example.com',
    ];
    
    return $data;
}, 10, 2);

```
