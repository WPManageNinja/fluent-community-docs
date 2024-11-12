# Configuring CloudFlare R2 in FluentCommunity Plugin

This guide will walk you through the process of configuring CloudFlare R2 for use with the FluentCommunity Plugin. You'll learn how to obtain the necessary credentials and input them into the plugin's settings.

## Prerequisites

- A CloudFlare account
- Access to the FluentCommunity Plugin in your WordPress installation

## Steps to Configure CloudFlare R2

### 1. Create a CloudFlare R2 Bucket

1. Log in to your CloudFlare account.
2. Navigate to "R2" under the "Storage" section.
3. Click "Create bucket" and choose a unique name for your bucket
    - Location: Choose the region closest to your target audience or use Automatic
    - Default Storage Class: Select Default

### 2. Generate API Tokens for R2

1. In your CloudFlare R2 dashboard, go to "Manage R2 API Tokens"
2. Click "Create API Token".
3. Give a name & From permissions, Select Object Read & Write.
4. From Specify bucket(s):
    - Select your newly created Bucket
5. TTL should be forever.
6. Click "Create API Token"
7. Now, Save the following Credential:
   1. Access Key ID
   3. Secret Access Key

### 3. Obtain R2 Endpoint

1. In the CloudFlare dashboard, go to "R2" > "Overview".
2. Select your bucket from the list of buckets.
3. Click on the "Settings" tab.
4. Scroll down to the "R2.dev subdomain" section and then click "allow access"
5. Copy the Public R2.dev Bucket URL

### 4. Configure FluentCommunity Plugin

1. In your WordPress admin panel, navigate to FluentCommunity Plugins > Settings > Features.
2. Find the CloudStorage Configaration Form.
3. Fill in the following fields:

    - **Access Key**: Paste the access key from your CloudFlare API token. (From step 2)
    - **Secret Key**: Paste the secret key from your CloudFlare API token. (From step 2)
    - **Account ID**: Paste the CloudFlare Account ID. (You will find it on R2 Overview page)
    - **Bucket**: Enter the name of the R2 bucket you created.
    - **Sub Folder** (Optional): If you want to store files in a specific subfolder within the bucket, enter the name here.
    - **Public URL** Add the public URL for your R2 bucket (From step 3)

4. Save your settings.

## Additional Configuration (Optional)

For added security or to manage multiple environments, you can define these values in your `wp-config.php` file:

```php
// CloudFlare R2 Configuration
define('FLUENT_COMMUNITY_CLOUD_STORAGE', 'cloudflare_r2');
define('FLUENT_COMMUNITY_CLOUD_STORAGE_ACCOUNT_ID', 'CLOUDFLARE_ACCOUNT_ID'); // like: 1718cb5a51e65c8f19e8sahdakh763
define('FLUENT_COMMUNITY_CLOUD_STORAGE_ACCESS_KEY', ''); // from step 2
define('FLUENT_COMMUNITY_CLOUD_STORAGE_SECRET_KEY', ''); // from step 2
define('FLUENT_COMMUNITY_CLOUD_STORAGE_BUCKET', 'YOUR_BUCKET_NAME'); // replace with your bucket name
define('FLUENT_COMMUNITY_CLOUD_STORAGE_PUBLIC_URL', 'https://pub-<YOUR_ACCOUNT_ID>.r2.dev'); // You can use the r2 custom domain too
define('FLUENT_COMMUNITY_CLOUD_STORAGE_SUB_FOLDER', 'community-files'); // optional or use your own folder name or keep it empty
```

If defined in `wp-config.php`, these values will override any settings in the plugin's configuration form.

## Troubleshooting

- Ensure that your API token has the correct permissions for R2 access.
- Double-check that the bucket name and public URL are correct.
- If using a custom domain, make sure it's properly configured in CloudFlare.

For further assistance, contact support team.
