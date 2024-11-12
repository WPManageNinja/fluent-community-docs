In the databases/Migrators directory, you can find the schema for the database.

`status: no-completed`

# Database Schema Documentation

This document outlines the database schema for the FluentCommunity plugin. The schema is defined in the `databases/Migrators` directory.

## Table: wp_fcom_post_comments

This table stores comments and reactions for posts in the community.

| Column Name       | Data Type         | Constraints           | Description                                    |
|-------------------|--------------------|-----------------------|------------------------------------------------|
| id                | BIGINT UNSIGNED    | PRIMARY KEY, AUTO_INCREMENT | Unique identifier for each comment       |
| user_id           | BIGINT UNSIGNED    | NULL                  | ID of the user who made the comment           |
| post_id           | BIGINT UNSIGNED    | NULL                  | ID of the post the comment belongs to         |
| parent_id         | BIGINT UNSIGNED    | NULL                  | ID of the parent comment (for nested comments)|
| reactions_count   | BIGINT UNSIGNED    | DEFAULT 0             | Number of reactions to this comment           |
| message           | LONGTEXT           | NULL                  | The comment text                              |
| message_rendered  | LONGTEXT           | NULL                  | Rendered version of the comment (e.g., HTML)  |
| meta              | LONGTEXT           | NULL                  | Additional metadata for the comment           |
| type              | VARCHAR(100)       | DEFAULT 'comment'     | Type of the entry (e.g., comment, reaction)   |
| content_type      | VARCHAR(100)       | DEFAULT 'text'        | Type of content (e.g., text, image)           |
| status            | VARCHAR(100)       | DEFAULT 'published'   | Status of the comment (e.g., published, draft)|
| is_sticky         | TINYINT(1)         | DEFAULT 0             | Whether the comment is sticky or not          |
| created_at        | TIMESTAMP          | NULL                  | Timestamp when the comment was created        |
| updated_at        | TIMESTAMP          | NULL                  | Timestamp when the comment was last updated   |

Indexes:
- `post_id`: For faster queries when fetching comments for a specific post
- `status`: For filtering comments by their status
- `type`: For filtering entries by their type

Note: The table uses the WordPress prefix (typically `wp_`) followed by `fcom_post_comments`.

Additional tables may exist in the `databases/Migrators` directory. To complete the documentation for all tables, you would need to review each migrator file in that directory and add their schemas to this document in a similar format.




## Table: wp_fcom_posts

This table stores posts and other content types in the community.

| Column Name       | Data Type         | Constraints           | Description                                    |
|-------------------|--------------------|-----------------------|------------------------------------------------|
| id                | BIGINT UNSIGNED    | PRIMARY KEY, AUTO_INCREMENT | Unique identifier for each post          |
| user_id           | BIGINT UNSIGNED    | NULL                  | ID of the user who created the post           |
| parent_id         | BIGINT UNSIGNED    | NULL                  | ID of the parent post (for nested content)    |
| title             | VARCHAR(192)       | NULL                  | Title of the post                             |
| slug              | VARCHAR(192)       | NULL                  | URL-friendly version of the title             |
| message           | LONGTEXT           | NULL                  | The post content                              |
| message_rendered  | LONGTEXT           | NULL                  | Rendered version of the post content          |
| type              | VARCHAR(100)       | DEFAULT 'feed'        | Type of the post (e.g., feed, article)        |
| content_type      | VARCHAR(100)       | DEFAULT 'text'        | Type of content (e.g., text, image)           |
| space_id          | BIGINT UNSIGNED    | NULL                  | ID of the space the post belongs to           |
| privacy           | VARCHAR(100)       | DEFAULT 'public'      | Privacy setting of the post                   |
| status            | VARCHAR(100)       | DEFAULT 'published'   | Status of the post (e.g., published, draft)   |
| featured_image    | TEXT               | NULL                  | URL or ID of the featured image               |
| meta              | LONGTEXT           | NULL                  | Additional metadata for the post              |
| is_sticky         | TINYINT(1)         | DEFAULT 0             | Whether the post is sticky or not             |
| comments_count    | INT(11)            | DEFAULT 0             | Number of comments on the post                |
| reactions_count   | INT(11)            | DEFAULT 0             | Number of reactions to the post               |
| priority          | INT(11)            | DEFAULT 0             | Priority of the post (for sorting)            |
| expired_at        | DATETIME           | NULL                  | Timestamp when the post expires               |
| scheduled_at      | DATETIME           | NULL                  | Timestamp when the post is scheduled to publish |
| created_at        | TIMESTAMP          | NULL                  | Timestamp when the post was created           |
| updated_at        | TIMESTAMP          | NULL                  | Timestamp when the post was last updated      |

Indexes:
- `user_id`: For faster queries when fetching posts by a specific user
- `slug`: For faster lookups when accessing posts by their slug
- `created_at`: For sorting posts by creation date
- `idx_space_id_status`: Composite index for filtering posts by space and status
- `idx_space_id_status_privacy`: Composite index for filtering posts by space, status, and privacy

Note: The table uses the WordPress prefix (typically `wp_`) followed by `fcom_posts`.


## wp_fcom_post_reactions

This table stores reactions to posts and comments in the community.

| Column Name       | Data Type         | Constraints           | Description                                    |
|-------------------|--------------------|-----------------------|------------------------------------------------|
| id                | BIGINT UNSIGNED    | PRIMARY KEY, AUTO_INCREMENT | Unique identifier for each reaction      |
| user_id           | BIGINT UNSIGNED    | NULL                  | ID of the user who reacted                    |
| post_id           | BIGINT UNSIGNED    | NULL                  | ID of the post that was reacted to            |
| comment_id        | BIGINT UNSIGNED    | NULL                  | ID of the comment that was reacted to         |
| reaction_type     | VARCHAR(100)       | NULL                  | Type of reaction (e.g., like, love, laugh)    |
| created_at        | TIMESTAMP          | NULL                  | Timestamp when the reaction was created       |
| updated_at        | TIMESTAMP          | NULL                  | Timestamp when the reaction was last updated  |

Indexes:
- `post_id`: For faster queries when fetching reactions for a specific post
- `comment_id`: For faster queries when fetching reactions for a specific comment
- `user_id`: For faster queries when fetching reactions by a specific user

Note: The table uses the WordPress prefix (typically `wp_`) followed by `fcom_post_reactions`.


## wp_fcom_spaces

This table stores information about spaces (communities or groups) within the platform.

| Column Name       | Data Type         | Constraints           | Description                                    |
|-------------------|--------------------|-----------------------|------------------------------------------------|
| id                | BIGINT UNSIGNED    | PRIMARY KEY, AUTO_INCREMENT | Unique identifier for each space         |
| name              | VARCHAR(192)       | NOT NULL              | Name of the space                              |
| slug              | VARCHAR(192)       | NULL                  | URL-friendly version of the space name         |
| description       | TEXT               | NULL                  | Description of the space                       |
| short_description | VARCHAR(255)       | NULL                  | Short description or tagline for the space     |
| type              | VARCHAR(100)       | DEFAULT 'public'      | Type of space (e.g., public, private)          |
| status            | VARCHAR(100)       | DEFAULT 'published'   | Status of the space (e.g., published, draft)   |
| featured_image    | TEXT               | NULL                  | URL or ID of the featured image for the space  |
| cover_image       | TEXT               | NULL                  | URL or ID of the cover image for the space     |
| meta              | LONGTEXT           | NULL                  | Additional metadata for the space              |
| members_count     | INT(11)            | DEFAULT 0             | Number of members in the space                 |
| posts_count       | INT(11)            | DEFAULT 0             | Number of posts in the space                   |
| created_by        | BIGINT UNSIGNED    | NULL                  | ID of the user who created the space           |
| created_at        | TIMESTAMP          | NULL                  | Timestamp when the space was created           |
| updated_at        | TIMESTAMP          | NULL                  | Timestamp when the space was last updated      |

Indexes:
- `slug`: For faster lookups when accessing spaces by their slug
- `type`: For filtering spaces by type
- `status`: For filtering spaces by status
- `created_by`: For faster queries when fetching spaces created by a specific user

Note: The table uses the WordPress prefix (typically `wp_`) followed by `fcom_spaces`.



## wp_fcom_space_users

This table manages the relationships between users and spaces, tracking membership and roles within each space.

| Column Name       | Data Type         | Constraints           | Description                                    |
|-------------------|--------------------|-----------------------|------------------------------------------------|
| id                | BIGINT UNSIGNED    | PRIMARY KEY, AUTO_INCREMENT | Unique identifier for each space-user relationship |
| space_id          | BIGINT UNSIGNED    | NOT NULL              | ID of the space                                |
| user_id           | BIGINT UNSIGNED    | NOT NULL              | ID of the user                                 |
| role              | VARCHAR(100)       | DEFAULT 'member'      | User's role in the space (e.g., member, admin) |
| status            | VARCHAR(100)       | DEFAULT 'active'      | Status of the user in the space                |
| meta              | LONGTEXT           | NULL                  | Additional metadata for the relationship       |
| joined_at         | TIMESTAMP          | NULL                  | Timestamp when the user joined the space       |
| updated_at        | TIMESTAMP          | NULL                  | Timestamp when the relationship was last updated |

Indexes:
- `space_id`: For faster queries when fetching users for a specific space
- `user_id`: For faster queries when fetching spaces for a specific user
- `role`: For filtering users by their role in spaces
- `status`: For filtering active or inactive memberships

Note: The table uses the WordPress prefix (typically `wp_`) followed by `fcom_space_users`.


## wp_fcom_media_archive

This table manages media files associated with various objects in the community platform.

| Column Name       | Data Type         | Constraints           | Description                                    |
|-------------------|--------------------|-----------------------|------------------------------------------------|
| id                | BIGINT UNSIGNED    | PRIMARY KEY, AUTO_INCREMENT | Unique identifier for each media entry   |
| object_source     | VARCHAR(100)       | NOT NULL              | Source of the object (e.g., post, comment)     |
| media_key         | VARCHAR(100)       | NOT NULL              | Unique key for the media file                  |
| user_id           | BIGINT             | NULL                  | ID of the user who uploaded the media          |
| feed_id           | BIGINT             | NULL                  | ID of the associated feed/post                 |
| is_active         | TINYINT(1)         | DEFAULT 0             | Whether the media is active or not             |
| sub_object_id     | BIGINT             | NULL                  | ID of a sub-object (e.g., comment ID)          |
| media_type        | VARCHAR(192)       | NULL                  | Type of media (e.g., image, video, document)   |
| driver            | VARCHAR(192)       | DEFAULT 'local'       | Storage driver (e.g., local, S3, R2)           |
| media_path        | TEXT               | NULL                  | Path or identifier of the media file           |
| media_url         | TEXT               | NULL                  | URL to access the media file                   |
| settings          | TEXT               | NULL                  | Additional settings or metadata                |
| created_at        | TIMESTAMP          | NULL                  | Timestamp when the entry was created           |
| updated_at        | TIMESTAMP          | NULL                  | Timestamp when the entry was last updated      |

Indexes:
- `is_active`: For filtering active media files
- `user_id`: For faster queries when fetching media for a specific user
- `media_key`: For quick lookups of media by its unique key
- `feed_id`: For faster queries when fetching media associated with a specific feed/post

Note: The table uses the WordPress prefix (typically `wp_`) followed by `fcom_media_archive`.



## wp_fcom_meta

This table stores metadata for various objects in the community platform.

| Column Name       | Data Type         | Constraints           | Description                                    |
|-------------------|--------------------|-----------------------|------------------------------------------------|
| id                | BIGINT UNSIGNED    | PRIMARY KEY, AUTO_INCREMENT | Unique identifier for each metadata entry |
| object_id         | BIGINT UNSIGNED    | NOT NULL              | ID of the associated object                    |
| object_type       | VARCHAR(100)       | NOT NULL              | Type of object (e.g., space, user, post)       |
| meta_key          | VARCHAR(255)       | NOT NULL              | Key for the metadata                           |
| meta_value        | LONGTEXT           | NULL                  | Value of the metadata                          |
| created_at        | TIMESTAMP          | DEFAULT CURRENT_TIMESTAMP | Timestamp when the entry was created       |
| updated_at        | TIMESTAMP          | NULL                  | Timestamp when the entry was last updated      |

Indexes:
- `object_id`: For faster queries when fetching metadata for a specific object
- `object_type`: For filtering metadata by object type
- `meta_key`: For quick lookups of specific metadata keys

Note: The table uses the WordPress prefix (typically `wp_`) followed by `fcom_meta`.



## wp_fcom_notifications

This table stores notifications for users in the community platform.

| Column Name       | Data Type         | Constraints           | Description                                    |
|-------------------|--------------------|-----------------------|------------------------------------------------|
| id                | BIGINT UNSIGNED    | PRIMARY KEY, AUTO_INCREMENT | Unique identifier for each notification  |
| user_id           | BIGINT UNSIGNED    | NOT NULL              | ID of the user receiving the notification      |
| type              | VARCHAR(100)       | NOT NULL              | Type of notification (e.g., comment, like)     |
| object_id         | BIGINT UNSIGNED    | NOT NULL              | ID of the associated object (e.g., post ID)    |
| object_type       | VARCHAR(100)       | NOT NULL              | Type of object (e.g., post, comment)           |
| actor_id          | BIGINT UNSIGNED    | NULL                  | ID of the user who triggered the notification  |
| content           | TEXT               | NULL                  | Content of the notification                    |
| is_read           | TINYINT(1)         | DEFAULT 0             | Whether the notification has been read         |
| created_at        | TIMESTAMP          | DEFAULT CURRENT_TIMESTAMP | Timestamp when the notification was created|
| updated_at        | TIMESTAMP          | NULL                  | Timestamp when the notification was updated    |

Indexes:
- `user_id`: For faster queries when fetching notifications for a specific user
- `type`: For filtering notifications by type
- `object_id`: For quicker lookups of notifications related to a specific object
- `is_read`: For filtering read/unread notifications

Note: The table uses the WordPress prefix (typically `wp_`) followed by `fcom_notifications`.


## wp_fcom_user_activities

This table tracks user activities within the community platform.

| Column Name       | Data Type         | Constraints           | Description                                    |
|-------------------|--------------------|-----------------------|------------------------------------------------|
| id                | BIGINT UNSIGNED    | PRIMARY KEY, AUTO_INCREMENT | Unique identifier for each activity      |
| user_id           | BIGINT UNSIGNED    | NOT NULL              | ID of the user performing the activity         |
| activity_type     | VARCHAR(100)       | NOT NULL              | Type of activity (e.g., post, comment, like)   |
| object_id         | BIGINT UNSIGNED    | NOT NULL              | ID of the associated object                    |
| object_type       | VARCHAR(100)       | NOT NULL              | Type of object (e.g., post, comment, space)    |
| content           | TEXT               | NULL                  | Additional content or context of the activity  |
| created_at        | TIMESTAMP          | DEFAULT CURRENT_TIMESTAMP | Timestamp when the activity occurred       |
| ip_address        | VARCHAR(45)        | NULL                  | IP address of the user when activity occurred  |

Indexes:
- `user_id`: For faster queries when fetching activities for a specific user
- `activity_type`: For filtering activities by type
- `object_id`: For quicker lookups of activities related to a specific object
- `created_at`: For chronological sorting and filtering

Note: The table uses the WordPress prefix (typically `wp_`) followed by `fcom_user_activities`.


## wp_fcom_xprofile

This table stores extended profile information for users in the community platform.

| Column Name       | Data Type         | Constraints           | Description                                    |
|-------------------|--------------------|-----------------------|------------------------------------------------|
| id                | BIGINT UNSIGNED    | PRIMARY KEY, AUTO_INCREMENT | Unique identifier for each profile entry |
| user_id           | BIGINT UNSIGNED    | NOT NULL, UNIQUE      | ID of the user associated with this profile    |
| total_points      | INT(11) UNSIGNED   | NOT NULL, DEFAULT 0   | Total points earned by the user                |
| username          | VARCHAR(100)       | NULL                  | User's chosen username                         |
| status            | ENUM               | NOT NULL, DEFAULT 'active' | User status (active, blocked, pending)    |
| is_verified       | TINYINT(1) UNSIGNED| NOT NULL, DEFAULT 0   | Whether the user is verified                   |
| display_name      | VARCHAR(192)       | NULL                  | User's display name                            |
| avatar            | TEXT               | NULL                  | URL or path to user's avatar image             |
| short_description | TEXT               | NULL                  | Brief description or bio of the user           |
| last_activity     | DATETIME           | NULL                  | Timestamp of user's last activity              |
| meta              | LONGTEXT           | NULL                  | Additional metadata in JSON format             |
| created_at        | TIMESTAMP          | NULL                  | Timestamp when the profile was created         |
| updated_at        | TIMESTAMP          | NULL                  | Timestamp when the profile was last updated    |

Indexes:
- `user_id`: For faster queries when fetching profile information for a specific user
- `username`: For quicker lookups and ensuring username uniqueness

Note: The table uses the WordPress prefix (typically `wp_`) followed by `fcom_xprofile`.

