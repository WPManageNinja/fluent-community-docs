### FluentCommunity Benchmark

**Live URL:** [https://fluentcommunity-test1.wp1.site/](https://fluentcommunity-test1.wp1.site/)

### Server Configuration
- Provider: xCloud Managed
- Package: Growing - xCloud (Managed)
- Price: $30 / Month
- Specs: 
  - RAM - 4 GB
  - SSD - 128 GB
  - vCPU - 2
  - Bandwidth - 3 TB


### Benchmark 1 (Without external Plugins)
- **Theme:** Default Theme (Twenty Twenty-Five)
- **Plugins:** FluentCommunity & FluentCommunity Pro
- **Object Cache:** Disabled
- **Page Caching:** Disabled
- **Posts/CPT Count:** 3 (default posts)

**Note:** Serber Location: US (New Jersey), Pingback Avg (From Asia): 38.65ms, PHP Version: 8.1, MySQL Version: 8.0.40-0ubuntu0.22.04.1, WordPress Version: 6.7.1

**REST API Benahchmarks**

| # | Users Count | Posts Count | Post Reactions | Comment Count | Comment Reactions | All Feeds Response (ms) | Space Posts Response (ms) | Members Index Response (ms) |
|---|-------------|-------------|----------------|---------------|-------------------|-------------------------|---------------------------|---------------------------|
| 1 | 0           | 0           | 0              | 0             | 0                 | 1.2 / 360               | 1.7 / 328                 | 1.3 / 344                 |
| 2 | 5,001       | 15,000      | 75,000         | 75,000        | 225,000           | 50.6 / 448              | 49.8 / 482                | 12.1 / 405                |
| 3 | 10,001      | 30,000      | 150,000        | 150,000       | 450,000           | 92.6 / 501              | 60.1 / 754                | 21.8 / 425                |
| 4 | 30,001      | 50,000      | 500,000        | 300,000       | 720,000           | 175 / 600               | 126.1 / 563               | 61.0 / 547                |
| 5 | 100,001     | 200,768     | 500,004        | 500,000       | 1,000,850         | 637 / 995               | 611.4 / 990               | 311.0 / 657               |

**Response Timing Definations:**

The first part is the execution time of the REST API request and the second part is total time taken including the network latency.

So `611.4 / 990` means the request took `611.4ms` to execute and `990ms` to complete including the network latency including execution time (Total).


### Benchmark 2 (With Standard Plugins & WordPress Contents)
- **Theme:** Kadence + Child Theme
- **Plugins:** 
  - FluentCommunity & FluentCommunity Pro
  - FluentCRM
  - FluentSMTP
  - FluentForms
  - WooCommerce
    - 1,000 Orders
    - 30 Demo Products
    - Other associate data with Orders and Products
  - LifterLMS (with 6 courses)
  - Regular Posts: 286
  - Published Pages: 10
- **Object Cache:** Disabled
- **Page Caching:** Disabled

**REST API Benahchmarks**

| # | Users Count | Posts Count | Post Reactions | Comment Count | Comment Reactions | All Feeds Response (ms) | Space Posts Response (ms) | Members Index Response (ms) |
|---|-------------|-------------|----------------|---------------|-------------------|-------------------------|---------------------------|-----------------------------|
| 1 | 100,001     | 200,768     | 500,004        | 500,000       | 1,000,850         | 648 / 1190              | 577 / 1050                | 200.1 / 711                 |

**Response Timing Definations:**

The first part is the execution time of the REST API request and the second part is total time taken including the network latency.

So `648 / 1190` means the request took `648ms` to execute and `1190ms` to complete including the network latency + execution time (Total).


#### Footnotes
- This benchmark is not conducted with live traffic and the server is standard configured by xCloud system default. No caching plugin is configured.
- The response time may vary based on the server location and network latency.
- Response time is measured using chrome network inspector and the average of 5 requests is taken.
- No other traffic is generated during the benchmark. But you are welcome to test the live site and share your feedback.
- We ran these benchmark to improve the performance of the FluentCommunity plugin and to make it more scalable for large communities.
