## Filter hooks available in FluentCommunity Plugin
`status: ongoing`

### Space Filters

##### `fluent_community/space/create_data`
- Description: Filters the data used to create a new space.
- Parameters:
  - `$data` (array): The data to be used for creating the space.
- Example:
  ```php
  add_filter('fluent_community/space/create_data', function($data) {
      // Modify or add data before space creation
      return $data;
  });
  ```

##### `fluent_community/space/update_data`
- Description: Filters the data used to update an existing space.
- Parameters:
  - `$data` (array): The data to be used for updating the space.
  - `$space` (object): The space object being updated.
- Example:
  ```php
  add_filter('fluent_community/space/update_data', function($data, $space) {
      // Modify update data before it's applied
      return $data;
  }, 10, 2);
  ```

##### `fluent_community/space/join_status_for_private`
- Description: Filters the join status for a private spaces. You can use this to allow users to join private spaces without approval.
- Parameters:
  - `$status` (string): The default join status ('pending').
  - `$space` (object): The original space object.
  - `$user` (object): The user object (Model).
- Example:
  ```php
  add_filter('fluent_community/space/join_status_for_private', function($status, $space, $user) {
      // Modify the status is required and return either 'pending' or 'active'
      // return 'active'; // for auto-approve
       
      return $status;
  }, 10, 3);
  ```

### Feed Filters

##### `fluent_community/feed/new_feed_data`
- Description: Filters the data used to create a new feed.
- Parameters:
  - `$data` (array): The data array for creating a new feed.
  - `$allData` (array): the full data array submitted by the user.
- Example:
  ```php
  add_filter('fluent_community/feed/new_feed_data', function($data, $allData) {
      // Modify the data before a new feed is created
      return $data;
  }, 10, 2);
  ```

##### `fluent_community/feed/update_data`
- Description: Filters the data used to update an existing feed.
- Parameters:
  - `$data` (array): The data array for creating a new feed.
  - `$feed` (object): The existing Feed model instance.
- Example:
  ```php
  add_filter('fluent_community/feed/update_data', function($data, $feed) {
      // Modify the data before a new feed is created
      return $data;
  }, 10, 2);
  ```

##### `fluent_community/max_post_length`
- Description: Filters the maximum length of a feed post.
- Parameters:
  - `$maxLength` (int): The default maximum char length (15000).
  
- Example:
  ```php
    add_filter('fluent_community/max_post_length', function($maxLength) {
        return 5000; // Set the maximum post length to 5000 characters
    });
    ```

### Comment Filters

##### `fluent_community/comment/comment_data`
- Description: Filters the data used to create a new comment.
- Parameters:
  - `$data` (array): The data array for creating a new comment.
  - `$feed` (object): The Feed model instance.
  - `$allData` (array): the full data array submitted by the user.
- Example:
  ```php
  add_filter('fluent_community/comment/comment_data', function($data, $feed, $allData) {
      // Modify the data before a new comment is created
      return $data;
  }, 10, 3);
  ```

##### `fluent_community/comment/update_comment_data`
- Description: Filters the data used to update an existing comment.
- Parameters:
  - `$data` (array): The data array for updating a comment.
  - `$comment` (object): The existing Comment model instance.
  - `$allData` (array): the full data array submitted by the user.
- Example:
  ```php
  add_filter('fluent_community/comment/update_comment_data', function($data, $comment, $allData) {
      // Modify the data before a comment is updated
      return $data;
  }, 10, 3);
  ```

### Helper Filters

##### `fluent_community/has_color_scheme`
- Description: Filter hook to enable or disable color scheme support.
- Parameters:
  - `$hasColorScheme` (boolean): The default color scheme support state.
- Example:
  ```php
  add_filter('fluent_community/has_color_scheme', function($hasColorScheme) {
      return false; // Disable color scheme support
  });
  ```

##### `fluent_community/super_admin_capability`
- Description: Filter hook to modify the capability required for super admin access.
- Parameters:
  - `$capability` (string): The default capability ('manage_options').
- Example:
  ```php
  add_filter('fluent_community/super_admin_capability', function($capability) {
      return 'custom_admin_capability';
  });
  ```

##### `fluent_community/is_rtl`
- Description: Filter hook to enable or disable RTL support.
- Parameters:
  - `$isRtl` (boolean): The default RTL support state.
- Example:
  ```php
    add_filter('fluent_community/is_rtl', function($isRtl) {
        return true; // Enable RTL support
    });
    ```

##### `fluent_community/has_global_post`
- Description: Filter hook to enable or disable global post support.
- Parameters:
  - `$hasGlobalPost` (boolean): The default global post support state.
- Example:
  ```php
    add_filter('fluent_community/has_global_post', function($hasGlobalPost) {
        return false; // Disable global post support
    });
    ```

##### `fluent_community/can_access_portal`
- Description: Filter hook to enable or disable portal access.
- Parameters:
  - `$canAccessPortal` (boolean): The default portal access state.
- Example:
  ```php
    /*
    * Please use this filter very carefully. If you return false, the user will not be able to access the portal.
    * You may also get locked out of the portal if you return false for everyone
    */
    add_filter('fluent_community/can_access_portal', function($canAccessPortal) {
        // check if the user can access to the portal or not and then return true or false
        return $canAccessPortal; 
    });
    ```

##### `fluent_community/menu_groups_for_user`
- Description: Filter hook to modify the menu groups for a user.
- Parameters:
  - `$menuGroups` (array): The default menu groups.
  - `$user` (object|null): The user object Model.
- Example:
  ```php
    add_filter('fluent_community/menu_groups_for_user', function($menuGroups, $user) {
        // Modify the menu groups based on user
        return $menuGroups;
    }, 10, 2);
    ```

##### `fluent_community/welcome_banner_for_logged_in`
- Description: Filter hook to modify the welcome banner for logged-in users.
- Parameters:
  - `$welcomeBanner` (array): The default welcome banner array.

- Example:
  ```php
    add_filter('fluent_community/welcome_banner_for_logged_in', function($welcomeBanner) {
        // Modify the welcome banner for logged-in users
        $welcomeBanner['title'] = 'Welcome to the community'; // Change the title
        $welcomeBanner['description_rendered'] = 'This is a custom welcome message'; // Change the description. You can use HTML here
        
        // return null to disable the welcome banner
        
        return $welcomeBanner;
    });
    ```

##### `fluent_community/welcome_banner_for_guests`
- Description: Filter hook to modify the welcome banner for guests (logged out users).
- Parameters:
  - `$welcomeBanner` (array): The default welcome banner array.
- Example:
  ```php
    add_filter('fluent_community/welcome_banner_for_guests', function($welcomeBanner) {
        // Modify the welcome banner for guests
        $welcomeBanner['title'] = 'Welcome to the community'; // Change the title
        $welcomeBanner['description_rendered'] = 'This is a custom welcome message'; // Change the description. You can use HTML here
        
        // return null to disable the welcome banner
        
        return $welcomeBanner;
    });
    ```

##### `fluent_community/convert_image_to_webp` 
- Description: Filter hook to enable or disable WebP conversion for images.
- Parameters:
  - `$convert` (boolean): The default WebP conversion state.
  - `$file` (array): The file array containing file information.
- Example:
  ```php
    add_filter('fluent_community/convert_image_to_webp', function($convert, $file) {
        // Disable WebP conversion based on file type
        if ($file['type'] === 'image/jpeg') {
            return false; // disable WebP conversion for JPEG images
        }
        
        return $convert; // Keep the default state for other file types
    }, 10, 2);
  
    // Disable WebP conversion for all images
    add_filter('fluent_community/convert_image_to_webp', '__return_false' ,10);
    ```
  
##### `fluent_community/media_upload_resize`
- Description: Filter hook to enable or disable media upload resizing.
- Parameters:
  - `$resize` (boolean): The default media upload resizing state.
  - `$file` (array): The file array containing file information.
- Example:
  ```php
    add_filter('fluent_community/media_upload_resize', function($resize, $file) {
        // Disable media upload resizing based on file type
        if ($file['type'] === 'image/png') {
            return false; // disable resizing for PNG images
        }
        
        return $resize; // Keep the default state for other file types
    }, 10, 2);
  
    // Disable media upload resizing for all images
    add_filter('fluent_community/media_upload_resize', '__return_false' ,10);
    ```
