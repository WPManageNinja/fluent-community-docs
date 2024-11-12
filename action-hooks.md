## Action hooks available in FluentCommunity Plugin
`status: ongoing`

## In this document:

- [Space Membership Actions](#space-membership-actions)
- [Space Actions](#space-actions)
- [Feed Actions](#feed-actions)
- [Comment Actions](#comment-actions)
- [Course - Student Related Actions](#course---student-related-actions)
- [Course Actions](#course-actions)
- [Leaderboard Actions](#leaderboard-actions)

### Space Membership Actions

##### `fluent_community/space/joined`

- Description: Fires after a user joins a space
- Parameters:
    - `$space` (object): The space object.
    - `$userId` (int): The user ID.
    - `$by` (string): The action that triggered the join. Can be `self` or `by_admin` or `by_automation`.
- Example:
  ```php
  add_action('fluent_community/space/joined', function($space, $userId, $by) {
      // Perform additional actions after user joins a space
      $role = $space->membership->role; // member or moderator or admin
      
  }, 10, 3);
  ```

##### `fluent_community/space/join_requested`

- Description: Fires after a user requests to join a space
- Parameters:
    - `$space` (object): The space object.
    - `$userId` (int): The user ID.
- Example:
  ```php
    add_action('fluent_community/space/join_requested', function($space, $userId) {
        // Perform additional actions after user requests to join a space
    }, 10, 2);
    ```

##### `fluent_community/space/user_left`

- Description: Fires after a user leaves a space
- Parameters:
    - `$space` (object): The space object.
    - `$userId` (int): The user ID.
    - `$by` (string): The action that triggered the leave. Can be `self` or `by_admin` or `by_automation`.
- Example:
  ```php
    add_action('fluent_community/space/user_left', function($space, $userId, $by) {
        // Perform additional actions after user leaves a space
    }, 10, 3);
    ```

### Space Actions

##### `fluent_community/space/created`

- Description: Fires after a new space is created.
- Parameters:
    - `$space` (object): The newly created space object.
    - `$data` (array): The data used to create the space.
- Example:
  ```php
  add_action('fluent_community/space/created', function($space, $data) {
      // Perform additional actions after space creation
  }, 10, 2);
  ```

##### `fluent_community/space/before_delete`

- Description: Fires before a space is deleted.
- Parameters:
    - `$space` (object): The space object being deleted.
- Example:
  ```php
  add_action('fluent_community/space/before_delete', function($space) {
      // Perform actions before space deletion
  });
  ```

##### `fluent_community/space/deleted`

- Description: Fires after a space is successfully deleted.
- Parameters:
    - `$spaceId` (int): The ID of the deleted space.
- Example:
  ```php
  add_action('fluent_community/space/deleted', function($spaceId) {
      // Perform cleanup or logging after space deletion
  });
  ```

##### `fluent_community/space/before_update`

- Description: Fires before a space is updated.
- Parameters:
    - `$space` (object): The space object being updated.
    - `$data` (array): The data to be updated.
- Example:
  ```php
  add_action('fluent_community/space/before_update', function($space, $data) {
      // Perform actions before space update
  }, 10, 2);
  ```

##### `fluent_community/space/updated`

- Description: Fires after a space is successfully updated.
- Parameters:
    - `$space` (object): The updated space object.
    - `$data` (array): The updated data.
- Example:
  ```php
  add_action('fluent_community/space/updated', function($space, $data) {
      // Perform actions after space update
  }, 10, 2);
  ```

### Feed Actions

##### `fluent_community/feed/created`

- Description: Action hook that fires after a new feed is created.
- Parameters:
    - `$feed` (object): The newly created feed object.
- Example:
  ```php
  add_action('fluent_community/feed/created', function($feed) {
      // Perform actions when a feed is created
  }, 10, 1);

##### `fluent_community/space_feed/created`

- Description: Action hook that fires after a new space feed is created.
- Parameters:
    - `$feed` (object): The newly created feed object.
- Example:
  ```php
  add_action('fluent_community/space_feed/created', function($feed) {
      // Perform actions when a space feed is created
      // You will find the space as $feed->space
  }, 10, 1);
  ```

##### `fluent_community/feed/updated`

- Description: Action hook that fires after a feed is updated.
- Parameters:
    - `$feed` (object): The updated feed object.
    - `$updateData` (array): The updated data.
- Example:
  ```php
    add_action('fluent_community/feed/updated', function($feed, $updateData) {
        // Perform actions when a feed is updated
    }, 10, 2);
    ```

##### `fluent_community/feed_mentioned`

- Description: Action hook that fires when a user / users are mentioned in a feed.
- Parameters:
    - `$feed` (object): The feed object where the mention was made.
    - `$mentionedUsers` Users Collections: The users mentioned in the feed.
- Example:
  ```php
    add_action('fluent_community/feed_mentioned', function($feed, $mentionedUsers) {
        // Perform actions when a user is mentioned in a feed
    }, 10, 2);
    ```

##### `fluent_community/feed/before_deleted`

- Description: Action hook that fires before a feed is deleted.
- Parameters:
    - `$feed` (object): The feed object being deleted.
- Example:
  ```php
    add_action('fluent_community/feed/before_deleted', function($feed) {
        // Perform actions before a feed is deleted
    }, 10, 1);
    ```

##### `fluent_community/feed/deleted`

- Description: Action hook that fires after a feed is deleted.
- Parameters:
    - `$feedId` (int): The ID of the deleted feed.
- Example:
  ```php
    add_action('fluent_community/feed/deleted', function($feedId) {
        // Perform actions after a feed is deleted
    }, 10, 1);
    ```

##### `fluent_community/feed/react_added`

- Description: Action hook that fires when a reaction is added to a feed.
- Parameters:
    - `$reaction` (object): The newly created reaction object.
    - `$feed` (object): The feed object that was reacted to.
- Example:
  ```php
  add_action('fluent_community/feed/react_added', function($reaction, $feed) {
      // Perform actions when a reaction is added
  }, 10, 2);
  ```

### Comment Actions

##### `fluent_community/comment_added`

- Description: Action hook that fires after a new comment is added.
- Parameters:
    - `$comment` (object): The newly created comment object.
    - `$feed` (object): The feed object that the comment was added to.
    - `$mentionedUsers` (array|null): The users mentioned in the comment (if any).
- Example:
  ```php
  add_action('fluent_community/comment_added', function($comment, $feed, $mentionedUsers) {
      // Perform actions when a comment is added
  }, 10, 3);
  ```

##### `fluent_community/comment_updated`

- Description: Action hook that fires after a comment is updated.
- Parameters:
    - `$comment` (object): The updated comment object.
    - `$feed` (object): The feed object that the comment was added to.
- Example:
  ```php
    add_action('fluent_community/comment_updated', function($comment, $feed) {
        // Perform actions when a comment is updated
    }, 10, 2);
    ```

##### `fluent_community/before_comment_create`

- Description: Action hook fired before a new comment is created.
- Parameters:
    - `$data` (array): The comment data to be inserted.
    - `$feed` (object): The associated Feed model instance.
- Example:
  ```php
  add_action('fluent_community/comment/before_create', function($data, $feed) {
      // Perform actions before comment creation
  }, 10, 2);
  ```

##### `fluent_community/before_comment_delete`

- Description: Action hook fired before a comment is deleted.
- Parameters:
    - `$comment` (object): The comment object being deleted.
- Example:
  ```php
    add_action('fluent_community/comment/before_delete', function($comment) {
        // Perform actions before comment deletion
    });
    ```

##### `fluent_community/comment_deleted`

- Description: Action hook fired after a comment is deleted.
- Parameters:
    - `$commentId` (int): The ID of the deleted comment.
    - `$feed` (object): The associated Feed model instance.
- Example:
  ```php
    add_action('fluent_community/comment/deleted', function($commentId, $feed) {
        // Perform actions after comment deletion
    }, 10, 2);
    ```

### Course - Student Related Actions

##### `fluent_community/course/enrolled`

- Description: Action hook that runs when a user is enrolled in a course.
- Parameters:
  - `$course` (object): The course object.
  - `$userId` (int): The user ID.
  - `$by` (string): The action that triggered the enrollment. Can be `self` or `by_admin` or `by_automation`.
- Example:
  ```php
  add_action('fluent_community/course/enrolled', function($user, $course) {
      // Perform actions when a user is enrolled in a course
  }, 10, 2);
  ```

##### `fluent_community/course/student_left`

- Description: Action hook that runs when a user is unenrolled from a course.
- Parameters:
  - `$course` (object): The course object.
  - `$userId` (int): The user ID.
  - `$by` (string): The action that triggered the enrollment. Can be `self` or `by_admin` or `by_automation`.
-
- Example:
  ```php
  add_action('fluent_community/course/student_left', function($user, $course) {
      // Perform actions when a user is unenrolled from a course
  }, 10, 2);
  ```

##### `fluent_community/course/completed`

- Description: Action hook that runs when a user completes a course.
- Parameters:
  - `$course` (object): The completed course object.
  - `$userId` (int): The user ID.
- Example:
  ```php
  add_action('fluent_community/course/completed', function($course, $userId) {
      // Perform actions when a user completes a course
  }, 10, 2);
  ```

##### `fluent_community/course/lesson_completed`

- Description: Action hook that runs when a user completes a lesson.
- Parameters:
  - `$lesson` (object): The completed lesson object.
  - `$userId` (int): The user ID.
- Example:
  ```php
    add_action('fluent_community/course/lesson_completed', function($lesson, $userId) {
        // Perform actions when a user completes a lesson
    }, 10, 2);
    ```

### Course Actions

##### `fluent_community/course/before_create`

- Description: Action hook that runs before a course is created.
- Parameters:
    - `$courseData` (array): The course data being submitted.
- Example:
  ```php
  add_action('fluent_community/course/before_create', function($courseData) {
      // Perform actions before course creation
  });
  ```

##### `fluent_community/course/created`

- Description: Action hook that runs after a course is created.
- Parameters:
    - `$course` (object): The newly created course object.
- Example:
  ```php
  add_action('fluent_community/course/created', function($course) {
      // Perform actions after course creation
  });
  ```

##### `fluent_community/course/updated`

- Description: Action hook that runs before a course is updated.
- Parameters:
    - `$course` (object): The course object being updated.
    - `$updateData` (array): The updated course data.
- Example:
  ```php
  add_action('fluent_community/course/updated', function($course, $updateData) {
      // Perform actions before course update
  }, 10, 2);
  ```

##### `fluent_community/course/published`

- Description: Action hook that runs after a course is published.
- Parameters:
    - `$course` (object): The course object.
- Example:
  ```php
    add_action('fluent_community/course/published', function($course) {
        // Perform actions after course is published
    });
    ```

##### `fluent_community/course/before_delete`

- Description: Action hook that runs before a course is deleted.
- Parameters:
    - `$course` (object): The course object being deleted.
- Example:
  ```php
  add_action('fluent_community/course/before_delete', function($course) {
      // Perform actions before course deletion
  });
  ```

##### `fluent_community/course/deleted`

- Description: Action hook that runs after a course is deleted.
- Parameters:
    - `$courseId` (int): The ID of the deleted course.
- Example:
  ```php
  add_action('fluent_community/course/deleted', function($courseId) {
      // Perform actions after course deletion
  });
  ```

##### `fluent_community/lesson/updated`

- Description: Action hook that runs when a user completes a lesson.
- Parameters:
    - `$lesson` (object): The Lesson object.
    - `$updateData` (array): The updated lesson data.
    - `$isNewlyPublished` (bool): Whether the lesson is newly published.
- Example:
  ```php
  add_action('fluent_community/lesson/updated', function($user, $updateData, $isNewlyPublished) {
      // Perform actions when a user completes a lesson
  }, 10, 3);
  ```

### Leaderboard Actions

##### `fluent_community/user_level_upgraded`

- Description: Action hook that runs when a user levels up in the leaderboard.
- Parameters:
    - `$xprofile` (object): The Community Profile object.
    - `$newLevel` (array): The upgraded Level array.
    - `$oldLevel` (array): The previous Level array.
- Example:
  ```php
  add_action('fluent_community/user_level_upgraded', function($xprofile, $newLevel, $oldLevel) {
      // Perform actions when a user levels up
      // $userId = $xprofile->user_id;
  }, 10, 3);
  ```
