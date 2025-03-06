# Configuring BunnyCDN in FluentCommunity Plugin

This guide provides two methods for configuring BunnyCDN with the FluentCommunity Plugin: using the plugin's UI and using WordPress's wp-config.php file.

## Prerequisites

- Bunny.net account
- The FluentCommunity Plugin installed and activated in your WordPress site

## Steps to Configure BunnyCDN

### 1. Create a Storage Zone

1. Log in to your Bunny.net Account.
2. Navigate to Storrage.
3. Click "Add Storage Zone" and choose a unique name for your Storage.
4. Select Storage Tier as your preference.
5. Select "Main Storage Region" based on your user's location.
### 2. Connect Pull Zone

1. Navigate to the "Connected Pull Zones" section From your Storage Zone you just created.
2. Click "Connect Pull Zone" and click "Add Pull Zone"
3. Give a Pull Zone Name name
4. Select "Storage Zone" as as your Storage Zone
5. Click "Add Pull Zone"

### 3. Copy The Password of the Storage Zone

1. Go to the Storage Zone you just created.
2. Click on the "FTP & API Access" tab.
3. Copy the password.

After this step you just need the following things:
- Password of Storage Zone
- Your Storage Zone Name
- Primary Storage Region of Storage Zone
- BunnyCDN Public URL (From the Pull Zone you just created. Chek Linked hostnames)

#### Option A: Using the Plugin UI

1. In your FluentCommunity panel, navigate to FluentCommunity Plugins > Settings > Features.
2. Find the CloudStorage Form and select BunnyCDN
3. Fill in the following fields:
    - **Storage Provider**: Select "BunnyCDN" from the dropdown menu.
    - **BunnyCDN API Key**: Paste the password of your Storage Zone.
    - **BunnyCDN Storage Zone Name**: Paste the Storage Zone Name
    - **Primary Storage Region**: Paste the Primary Storage Region
    - **BunnyCDN Public URL**: Paste the BunnyCDN Public URL. Make sure you add the https:// at the beginning.
4. Click "Save Changes" to store your settings.

#### Option B: Using wp-config.php

Add the following definitions to your `wp-config.php` file, adjusting the values according to your Amazon S3 setup:

```php
// Amazon BunnyCDN Configuration
define('FLUENT_COMMUNITY_CLOUD_STORAGE', 'bunny_cdn');
define('FLUENT_COMMUNITY_CLOUD_STORAGE_S3_REGION', 'storage.bunnycdn.com'); //  change with your region.check the next section
define('FLUENT_COMMUNITY_CLOUD_STORAGE_ACCESS_KEY', 'PASSWORD'); // Your Storage Zone Password
define('FLUENT_COMMUNITY_CLOUD_STORAGE_BUCKET', 'STORAGE_ZONE_NAME'); // Your Storage Zone Name
define('FLUENT_COMMUNITY_CLOUD_STORAGE_PUBLIC_URL', 'https://PULL_ZONE.b-cdn.net'); // Your BunnyCDN Public URL
```


**Maps for `FLUENT_COMMUNITY_CLOUD_STORAGE_S3_REGION`**

Please use the value for `FLUENT_COMMUNITY_CLOUD_STORAGE_S3_REGION` based on the region you selected when creating your Storage Zone:
- Falkenstein, DE => `storage.bunnycdn.com`
- London, UK => `uk.storage.bunnycdn.com`
- New York, US => `ny.storage.bunnycdn.com`
- Los Angeles, US => `la.storage.bunnycdn.com`
- Singapore, SG => `sg.storage.bunnycdn.com`
- Stockholm, SE => `se.storage.bunnycdn.com`
- São Paulo, BR => `br.storage.bunnycdn.com`
- Johannesburg, SA => `jh.storage.bunnycdn.com`
- Sydney, SYD => `syd.storage.bunnycdn.com`


## Notes

- If you use both methods, the wp-config.php settings will take precedence over the UI settings.
- The UI method is more user-friendly and doesn't require direct file access to your WordPress installation.
- The wp-config.php method is more secure as it keeps sensitive information out of the database.
- Ensure that all the credentials are correctly entered, regardless of the method you choose.


## Limitations
As BunnyCDN is not a full S3 compatible storage and does not support ACL. If you use Document upload feature then the full URL will still be served via the CDN.

## Troubleshooting
For further assistance, contact the support team.
