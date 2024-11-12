# Configuring Amazon S3 in FluentCommunity Plugin

This guide provides two methods for configuring Amazon S3 with the FluentCommunity Plugin: using the plugin's UI and using WordPress's wp-config.php file.

## Prerequisites

- An Amazon Web Services (AWS) account
- The FluentCommunity Plugin installed and activated in your WordPress site

## Steps to Configure Amazon S3

### 1. Create an Amazon S3 Bucket

1. Log in to your AWS Management Console.
2. Navigate to the S3 service.
3. Click "Create bucket" and choose a unique name for your bucket.
4. Make sure you disable "**Block all public access**"
5. From the Ownership section, enable "**ACLs enabled**" and from "Object Ownership" select "**Object Writer**"
4. Configure the bucket settings as needed, ensuring appropriate permissions for your use case. (You may keep everything as default).

### 2. Create an IAM User for Access

1. In the AWS Management Console, go to the IAM (Identity and Access Management) service.
2. Click "Users" in the left sidebar, then "Add user".
3. Choose a username and select "Programmatic access" for the access type. Or do not select (Provide user access to the AWS Management Console - optional)
4. For permissions, you can either:
    - Attach the `AmazonS3FullAccess` policy directly.
    - Create a custom policy with more restricted permissions (if needed).
5. Complete the user creation process.
6. Now go to the user's details page and click on the "**Security credentials**" tab and then find **Access keys** section
7. Click "**Create access key**" and note down the Access Key ID and Secret Access Key.
8. Select Other options in the "Access key best practices & alternatives" screen
9. Now copy the Access Key ID and Secret Access Key and keep them secure. (You will need these to configure the plugin)

### 3. Configure FluentCommunity Plugin

You have two options for configuring the plugin: using the UI or using wp-config.php.

#### Option A: Using the Plugin UI

1. In your FluentCommunity panel, navigate to FluentCommunity Plugins > Settings > Features.
2. Find the CloudStorage Form.
3. Fill in the following fields:
    - **Storage Provider**: Select "Amazon S3" from the dropdown menu.
    - **Access Key**: Paste the Access Key ID from your IAM user.
    - **Secret Key**: Paste the Secret Access Key from your IAM user.
    - **Bucket**: Enter the name of your S3 bucket.
    - **Sub Folder** (Optional): If you want to store files in a specific subfolder within the bucket, enter the path here.
4. Click "Save Changes" to store your settings.

#### Option B: Using wp-config.php

Add the following definitions to your `wp-config.php` file, adjusting the values according to your Amazon S3 setup:

```php
// Amazon S3 Configuration
define('FLUENT_COMMUNITY_CLOUD_STORAGE', 'amazon_s3');
define('FLUENT_COMMUNITY_CLOUD_STORAGE_REGION', 'us-east-1'); // change with your region. If it's global just remove this line or keep it empty
define('FLUENT_COMMUNITY_CLOUD_STORAGE_ACCESS_KEY', '********************');
define('FLUENT_COMMUNITY_CLOUD_STORAGE_SECRET_KEY', '********************');
define('FLUENT_COMMUNITY_CLOUD_STORAGE_BUCKET', 'your-bucket-name'); // change with your bucket name
define('FLUENT_COMMUNITY_CLOUD_STORAGE_SUB_FOLDER', 'site-name'); // optional. If you want to store the files in a subfolder of that bucket
 ```

Replace the placeholder values with your actual Amazon S3 credentials and information.

## Notes

- If you use both methods, the wp-config.php settings will take precedence over the UI settings.
- The UI method is more user-friendly and doesn't require direct file access to your WordPress installation.
- The wp-config.php method is more secure as it keeps sensitive information out of the database.
- Ensure that all the credentials are correctly entered, regardless of the method you choose.
- The sub-folder setting is optional and can be used if you want to organize your files within the bucket.

## Troubleshooting

- If you encounter permission issues, review your bucket policy and IAM user permissions.
- Ensure that your S3 bucket is in the correct region and that it's accessible from your WordPress server.
- Check that your access key and secret key are entered correctly without any extra spaces.

For further assistance, contact the support team.
