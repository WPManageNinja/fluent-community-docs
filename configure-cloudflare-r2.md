---
title: Configuring CloudFlare R2 in FluentCommunity Plugin
slug: configure-cloudflare-r2
tagline: CloudFlare R2 Integration with FluentCommunity Plugin
sidebar: true
prev: true
next: true
editLink: true
pageClass: docs-home
menu_order: 1
---

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

### 2. Generate API Tokens

1. In your CloudFlare dashboard, go to "My Profile" > "API Tokens".
2. Click "Create Token".
3. Select "Create Custom Token".
4. Set the following permissions:
    - Account > R2 > Edit
    - Account > R2 Storage > Edit
5. Set the "Account Resources" to include your specific account.
6. Create the token and save the displayed credentials securely.

### 3. Obtain R2 Endpoint

1. In the CloudFlare dashboard, go to "R2" > "Overview".
2. Look for the "R2 API" section.
3. Copy the endpoint URL (e.g., `https://<ACCOUNT_ID>.r2.cloudflarestorage.com`).

### 4. Configure FluentCommunity Plugin

1. In your WordPress admin panel, navigate to FluentCommunity Plugins > Settings > Features.
2. Find the CloudStorage Configaration Form.
3. Fill in the following fields:

    - **Access Key**: Paste the access key from your CloudFlare API token.
    - **Secret Key**: Paste the secret key from your CloudFlare API token.
    - **Account ID**: Paste the CloudFlare Account ID.
    - **Bucket**: Enter the name of the R2 bucket you created.
    - **Sub Folder** (Optional): If you want to store files in a specific subfolder within the bucket, enter the name here.
    - **Public URL** Add the public URL for your R2 bucket (e.g., `https://pub-<ACCOUNT_ID>.r2.dev`).

4. Save your settings.

## Additional Configuration (Optional)

For added security or to manage multiple environments, you can define these values in your `wp-config.php` file:

```php
// CloudFlare R2 Configuration
define('FLUENT_COMMUNITY_CLOUD_STORAGE', 'cloudflare_r2');
define('FLUENT_COMMUNITY_CLOUD_STORAGE_ACCOUNT_ID', 'ACCOUNT_ID'); // like: 1718cb5a51e65c8f19e8sahdakh763
define('FLUENT_COMMUNITY_CLOUD_STORAGE_ACCESS_KEY', 'ACCESS_KEY_HERE');
define('FLUENT_COMMUNITY_CLOUD_STORAGE_SECRET_KEY', 'SECRET_KEY_HERE');
define('FLUENT_COMMUNITY_CLOUD_STORAGE_BUCKET', 'BUCKET_NAME');
define('FLUENT_COMMUNITY_CLOUD_STORAGE_PUBLIC_URL', 'https://pub-SOME_RANDOM_STRINGS.r2.dev'); // You can use the r2 custom domain too
define('FLUENT_COMMUNITY_CLOUD_STORAGE_SUB_FOLDER', 'my-site-name'); // optional
```

If defined in `wp-config.php`, these values will override any settings in the plugin's configuration form.

## Troubleshooting

- Ensure that your API token has the correct permissions for R2 access.
- Double-check that the bucket name and public URL are correct.
- If using a custom domain, make sure it's properly configured in CloudFlare.

For further assistance, contact support team.
