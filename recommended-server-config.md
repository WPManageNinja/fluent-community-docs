## Recommended Server Configuration for FluentCommunity

### Introduction
FluentCommunity was built to be fast and efficient. In this document, we will discuss how FluentCommunity was built and what you can do to keep your community fast and efficient.

### Why FluentCommunity is so fast and efficient?
We built FluentCommunity with performance in mind. Every feature we developed is optimized to be fast and efficient. Here are some of the reasons why FluentCommunity is so fast and efficient:

- **Built with VueJS:** We use VueJS for the frontend of FluentCommunity. VueJS is a lightweight and fast JavaScript framework that helps us build fast and responsive interfaces. The whole application is actually a single-page application (SPA) which means that the page doesn't reload when you navigate between different sections of the site. This makes the site feel faster and more responsive.
- **Custom Database Tables:** We use custom database tables to store data. We also made sure the internal database schema is optimized for performance. [View the Database Schema](database-schema.md)
- **Optimized Queries:** We optimized all the database queries to make sure they are fast and efficient.
- **Object Caching:** We use object caching for the most frequently used data, like different settings. This helps us reduce the number of database queries and improve performance.
- **Lazy Loading:** We use lazy loading for images and other assets. This helps us reduce the initial load time of the site.
- **Background Job Processing:** We smartly handle long jobs like sending email notifications when a user posts new content or leaves a comment. We use background job processing so the user doesn't have to wait for the job to complete.
- **Super Optimized Media Handling:** We resize and convert all the uploaded images to WebP format. This helps us reduce the image size and improve performance.

However, there are some server configurations that can help you get the most out of your site. The next sections will guide you through the recommended server configuration and settings for FluentCommunity.

### Recommended Server Software Configuration
- **PHP Version**: We recommend using PHP 8.1 or higher.
- **MySQL Version**: MySQL version 8.0 or greater OR MariaDB version 10.5 or greater.
- **Web Server**: We recommend using Nginx.
- **Object Cache**: We recommend using Redis for object caching.

### Server-Side CRON
FluentCommunity processes all the notification emails as scheduled actions. To make sure that the emails are sent on time and efficiently, you should set up a server-side CRON job for your WordPress.

**Related Documentation**:
[Setting up Server-Side CRON job for WordPress](https://fluentcrm.com/docs/fluentcrm-cron-job-basics-and-checklist/)

PS: If you are using [xCloud.host](https://xcloud.host/) or similar modern hosting panel, it will be enabled by default.

### Media Storage
FluentCommunity Pro allows you to store media files in Amazon S3 / Cloudflare R2. If you have an active community with lots of media files, you should definitely consider using Amazon S3 or Cloudflare R2 for media storage. As both Amazon S3 and Cloudflare R2 are great, we suggest using Cloudflare R2 as it's more cost-effective and faster.

- [Configure Cloudflare R2 for Media Storage](configure-cloudflare-r2.md)
- [Configure Amazon S3 for Media Storage](configure-amazon-s3.md)

### Recommended Server Hardware
We strongly recommend using a VPS or Cloud server and highly discourage the use of shared hosting for FluentCommunity. You should not use shared hosting for any WordPress websites.

- **CPU**: 2 Cores or more
- **RAM**: 4GB or more
- **Storage Type**: NVMe SSD

### Hosting Providers We Recommend
We run our own community on [xCloud.host](https://xcloud.host/) and we highly recommend them. They are fast, reliable, and have great support. They also have great pricing.

xCloud also has all the necessary features like Redis, Object Cache, Server-Side CRON, etc., enabled by default. Their servers are optimized for WordPress.

### Other Hosting Providers you may use:
- GridPane
- RunCloud
- Cloudways
