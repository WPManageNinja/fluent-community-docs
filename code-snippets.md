# Useful Code Snippets for FluentCommunity Plugin

This documentation provides a collection of useful code snippets for developers working with the FluentCommunity Plugin or just customize the portal's default behavior. These snippets can help you customize and extend the functionality of the plugin to meet your specific needs. We recommend to use [FluentSnippet plugin](https://wordpress.org/plugins/easy-code-manager/) to manage these snippets.


### Modify Portal URL Slug<a name="portal_slug"></a>
By default the portal URL is `/portal`. You can also change from the admin settings. If you want to change the portal URL slug programmatically, you can use the following code. 

```php
define('FLUENT_COMMUNITY_PORTAL_SLUG', 'community');
```


If you want to make the portal as your homepage, you can use the following code. 
Please note that, this will not work if your WordPress installation is in a subdirectory. The WordPress installation should be in the root directory of our domain or sub domain. 
```php
define('FLUENT_COMMUNITY_PORTAL_SLUG', '');
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

#### Check if a specific feature module is enabled<a name="check_feature_module"></a>
You can check if a specific feature module is enabled using the following code. 

```php
$featureModule = 'course_module'; // leader_board_module, course_module, giphy_module, emoji_module, cloud_storage, user_badge
if(\FluentCommunity\App\Services\Helper::isFeatureEnabled($featureModule)) {
    // Feature is enabled
} else {
    // Feature is disabled
}
```

## User Space Related Snippets

#### Add a user to a space<a name="add_user_to_space"></a>
You can add a user to a space using the following code. Please make sure you use the code in your own function. 

```php

$spaceId = 1; // 1 is the space id
$userId = 1; // 1 is the user id
$role = 'member'; // member, moderator, admin
$by = 'by_admin'; // 'by_admin' or 'self';
\FluentCommunity\App\Services\Helper::addToSpace($spaceId, $userId, $role, $by);
```

#### Remove a user from a space<a name="remove_user_from_space"></a>
You can remove a user from a space using the following code. Please make sure you use the code in your own function. 
Return true if added, false if the member is already in the space or no user or space found in the system.

```php
\FluentCommunity\App\Services\Helper::removeFromSpace($spaceId, $userId, 'by_admin');
```

#### Get list of space_ids a user is member in<a name="get_user_space_ids"></a>
You can get the list of space ids a user is in using the following code. Please make sure you use the code in your own function.

```php
$userId = 1; // 1 is the user id
$spaceIds = \FluentCommunity\App\Services\Helper::getUserSpaceIds($userId); // this will return array of space ids
```

#### Get list of spaces a user in<a name="get_user_spaces"></a>
You can get the list of spaces a user is in using the following code. Please make sure you use the code in your own function.

```php
$userId = 1; // 1 is the user id
$spaces = \FluentCommunity\App\Services\Helper::getUserSpaces($userId); // this will return Collection of Space objects
```

#### Get list of spaces in the site <a name="get_all_spaces"></a>
You can get the list of spaces in the site using the following code. Please make sure you use the code in your own function.

```php

/*
 * Get all spaces (including published and draft)
 * @param boolean $byGroup - true to get spaces by group
 * @return Collection
 */
$spaces = \FluentCommunity\App\Functions\Utility::getSpaces($byGroup); // this will return Collection of Space objects
```

### Course Related Snippets    

#### Add a user to a course<a name="add_user_to_course"></a>
You can add a user to a course using the following code. Please make sure you use the code in your own function.

```php
$courseId = 1; // 1 is the course id
$userId = 1; // 1 is the user id

\FluentCommunity\Modules\Course\Services\CourseHelper::enrollCourse($courseId, $userId);
```

#### Remove a user from a course<a name="remove_user_from_course"></a>
You can remove a user from a course using the following code. Please make sure you use the code in your own function.
    
```php
$courseId = 1; // 1 is the course id
$userId = 1; // 1 is the user id
\FluentCommunity\Modules\Course\Services\CourseHelper::leaveCourse($courseId, $userId);
```

#### Add a user to multiple courses<a name="add_user_to_courses"></a>
You can add a user to multiple courses using the following code. Please make sure you use the code in your own function.

```php
$courseIds = [1, 2, 3]; // 1, 2, 3 are the course ids
$userId = 1; // 1 is the user id
\FluentCommunity\Modules\Course\Services\CourseHelper::enrollCourses($courseIds, $userId);
```

#### Remove a user from multiple courses<a name="remove_user_from_courses"></a>
You can remove a user from multiple courses using the following code. Please make sure you use the code in your own function.

```php
$courseIds = [1, 2, 3]; // 1, 2, 3 are the course ids
$userId = 1; // 1 is the user id
\FluentCommunity\Modules\Course\Services\CourseHelper::leaveCourses($courseIds, $userId);
```

#### Get the list of courses a user is enrolled in<a name="get_user_courses"></a>
You can get the list of courses a user is enrolled in using the following code. Please make sure you use the code in your own function.

```php
$userId = 1; // 1 is the user id
$courses = \FluentCommunity\Modules\Course\Services\CourseHelper::getUserCourses($userId); // this will return Collection of Course objects
```



#### Get list of courses in the site <a name="get_all_courses"></a>
You can get the list of courses in the site using the following code. Please make sure you use the code in your own function.

```php

/*
 * Get all spaces (including published and draft)
 * @param boolean $byGroup - true to get courses by group
 * @return Collection
 */
$spaces = \FluentCommunity\App\Functions\Utility::getCourses($byGroup); // this will return Collection of Space objects
```

### Feed-Related Snippets

#### Create a new post programatically<a name="create_new_feed"></a>

You can create a new post programatically using the following code. Please make sure you use the code in your own function.

```php
$feedData = [
    'title' => 'Post Title',
    'message' => 'Post Content', // in markdwon format.
    'space_id' => 1, // 1 is the space id
    'user_id' => 1, // 1 is the user id
];

try {
    $feed = \FluentCommunity\App\Services\FeedsHelper::createFeed($feedData); // this will return $feed Model object
} catch (\Exception $e) {
    // handle the exception
}
```


### Community Profile Related Snippets

#### Get the profile Model<a name="get_user_profile"></a>

You can get the profile model of a user using the following code. Please make sure you use the code in your own function.

```php
$userId = 1; // 1 is the user id
$profile = \FluentCommunity\App\Services\ProfileHelper::getProfile($userId); // this will return $profile Model object or null if profile is not ccreated

if($profile) {
    $profileSpaces = $profile->spaces;
    $profileCourses = $profile->courses;
}
```

**Profile Model Properties**
- id
- user_id
- total_points
- username
- status
- is_verified
- display_name
- avatar
- short_description
- last_activity
- meta
- created_at
- updated_at

- user // Will return User Model
- spaces // Will return Collection of Space Models that the user is member in
- courses // Will return Collection of Course Models that the user is enrolled in
- posts // Will return Collection of Feed Models that the user has posted

**Profile Model Methods**
- getCrmContact() // Will return the CRM contact object if FluentCRM exist and the user is a contact
- getCompletionScore() // Will return the profile completion score

