---
created: 2023-09-04 15:04
modified: Monday 4th September 2023 15:04:30

---
up:: [[01 System Design Problems]]
tags:: [[system-design]]

### What is it?
A robot often used by search engines to discover new or updated content to the web by collecting a few pages and recursively following the links on those pages to collect new content.
1. Given a set of URLs download the web pages addressed by the URLs.
2. Extract the URLs from the web pages
3. Add new URLs to the list of URLs to downloaded, repeat these 3 steps recursively.


### Functional Requirements

1. **What is the purpose of this web crawler?
	- Web mining, Web monitoring, **Search indexing**
2. how many pages should it be able to crawl a month?
	- 1 billion
3. do we need to store the crawled pages?
	- yes
4. how should duplicate content be handled?
	- duplicates should be ignored

### Non-Functional Requirements
1- Scalability
2- Robust: should handle edge cases such as unresponsive servers, bad HTML, crashes, malicious links
3- Politeness: should not make too many requests to a website within a short period of time
4- Extensible: can easily be modified to support new content types

### High Level Design
![[Screenshot 2023-09-04 at 4.08.21 PM.png]]
### Parts of a web crawler
**Seed URLs**: starting point for the crawl process. For example, to crawl the web pages from a university website you may select the university's domain name as the seed URL
A good seed URL serves as a good starting point where the crawler can use many links
**URL Frontier**: Queue that pulls from the seed URLs and groups the incoming URLs into 2, already downloaded or to be downloaded.
**HTML Downloader**: Downloads web pages from the internet provided by the URL frontier.
**DNS Resolver**: In order to download the webpage we need the IP address, so the HTML downloader calls a DNS resolver to translate the URL to the IP address
**Content Parser**: After it is downloaded the content parser validates the web pages, ignores malformed web pages or data noise to prevent wasting storage. After content is parsed and validated, it is passed to the “Content Seen?” component.
	Some of the contents have little or no value, such as advertisements, code snippets, spam URLs, etc. Those contents are not useful for crawlers and should be excluded if possible.
**Content Seen**: This component removes duplicate contents. We can compare the hash values of the 2 web pages. Hashes or checksums help to detect duplication. “Content Seen” component checks if a HTML page is already in the storage.
	• If it is in the storage, this means the same content in a different URL has already been processed. In this case, the HTML page is discarded.
	• If it is not in the storage, the system has not processed the same content before. The content is passed to Link Extractor.
**Content Storage**: storage system for HTML content,
**URL extractor**: parses and extracts links from the stored HTML pages,
**URL Filter**: excludes certain content types, file extensions, errors links and URLs of black listed sites
**URL seen**: data structure that keeps tracks of URL that are visited before or already in frontier, helps avoid adding the same URL multiple times. Component checks if a URL is already in the storage, if yes, it is processed before, and nothing needs to be done.
**URL storage**: storage of already visited URL's, if a URL has not been processed before, this new URL is added to the URL Frontier.
**Extension Module**: Large scale systems are constantly evolving, we want to make the system flexible enough to easily support new content types. Our system can be easily extended by plugging the new modules.
	• PNG Downloader module is plugged-in to download PNG files.
	• Web Monitor module is added to monitor the web and prevent copyright and trademark infringements.


### [[Depth First Search]] vs [[Breath First Search]]
BFS is commonly used by web crawlers, because the depth of a DFS can be very deep. However, the issue with DFS is that most links on the same web page are linked back to the same host, therefore when a web crawler tries to download a webpage in parallel the host will be flooded with request. This is impolite

### URL frontier
Stores URLs to be downloaded, the URL frontier ensure **politeness**, prioritize, freshness

### HTML Downloader
Downloads web pages from the internet using the HTTP protocol

Robots.txt, robots exclusion protocol, this is how website communicate with crawlers, and specifies what pages crawlers are allowed to download,
Performance Optimization of a downloader
1. **Distributed crawl**: crawl jobs are distributed into multiple servers, and each server runs multiple threads. The URL space is partitioned into smaller pieces; so, each downloader is responsible for a subset of the URLs.
3. Cache DNS Resolver: DNS Resolver is a bottleneck for crawlers because DNS requests might take time due to the synchronous nature of many DNS interfaces. Maintaining our DNS cache to avoid calling DNS frequently is an effective technique for speed optimization. Our DNS cache keeps the domain name to IP address mapping and is updated periodically by cron jobs.
4. Locality: Distribute crawl servers geographically. When crawl servers are closer to website hosts, crawlers experience faster download time.
5. Short timeout: Some web servers respond slowly or may not respond at all. To avoid long wait time, a maximal wait time is specified. If a host does not respond within a predefined time, the crawler will stop the job and crawl some other pages.
### Robustness
**Consistent hashing:** distribute the load among downloaders
Save crawl states and data: guard against failures, a distributed crawl can be restarted by loading saved states and data
Exception handling: errors are inevitalble the crawler should handle exceptions without crashing the system
Data validation: prevent system errors by parsing and validating the web pages contents

### Spider Traps
A spider trap is a web page that causes a crawler in an infinite loop. Such spider traps can be avoided by setting a maximal length for URLs.
