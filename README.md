# **Web Scraping with Scrapy and MongoDB**

## **Overview**
This project demonstrates a complete web scraping pipeline using the Scrapy framework, with MongoDB as a flexible data storage solution. Targeting the "Books to Scrape" demo site, the scraper efficiently extracts book details and stores them for analysis. A dedicated Python virtual environment was used and is recommended to manage dependencies.

## **Features**
- **Scrapy Framework**: Designed for efficient, asynchronous web scraping with structured project files and reusable spider configurations.
- **MongoDB Integration**: Utilizes MongoDB for scalable data storage, storing scraped data in a JSON-like structure.
- **Project Structure**: Organized with Scrapy’s auto-generated files, alongside custom spider, item, and pipeline configurations.

## **Getting Started**

### **Inspecting the Target Site**
Used browser developer tools to locate and inspect target elements, such as titles, prices, and URLs. This step allows refinement of CSS selectors for accurate data extraction.

### **Scrapy Shell**
Used Scrapy’s shell to test CSS selectors, preview extracted data, and confirm the accuracy of data fields. Adjusted selectors as needed for optimal scraping performance.

### **Building and Configuring the Spider**
1. **Defining Item Class**: Structured data fields (`url`, `title`, `price`) in a custom `BooksItem` class to manage scraped content effectively.
2. **Generating the Spider**: Used `scrapy genspider` to create a spider structure, defining `start_urls` and `parse()` methods to handle data extraction.
3. **Handling Pagination**: Configured the spider to follow pagination links using `response.urljoin` for recursive data extraction across multiple pages.

## **Database Configuration**
1. **Installing and Setting Up MongoDB**: Initialized MongoDB locally, creating a `books_db` database and `books` collection to store scraped records.
2. **Connecting to MongoDB**: Used `pymongo` to connect Scrapy to MongoDB, defining connection details in `settings.py`.

## **Data Processing Pipeline**
Implemented a custom pipeline in `pipelines.py` to handle data transformation and loading, storing each item in MongoDB.

### **Duplicate Handling**
Prevented duplicate entries using URL hashing, with an optional upsert operation to update existing documents when necessary.

## **Debugging and Testing**

- **Custom Logging**: Leveraged Scrapy’s logger to track spider activity and set log levels in `settings.py` to manage output.
- **Error Handling with `errback`**: Defined an `errback` function to handle network errors gracefully, ensuring uninterrupted scraping.
- **Spider Contracts**: Added contracts directly in docstrings to validate the spider’s output (items, requests, fields) with minimal setup.
- **Writing Unit Tests**: Used Python’s `unittest` to test components like parsing and pagination handling, ensuring scraper reliability.

## **Handling Advanced Scraping Scenarios**

- **Retrying Middleware**: Customized `RetryMiddleware` in `settings.py` to handle errors like HTTP 500 and 429, ensuring stable scraping sessions.
- **Scraping Dynamic Content**: For JavaScript-rendered pages, explored alternatives like API requests, `scrapy-splash` for JavaScript rendering, or browser automation with `scrapy-playwright`.
- **Anti-Scraping Measures**: Configured settings for rotating `User-Agent`, using proxies, adding `DOWNLOAD_DELAY`, and respecting `robots.txt` to avoid bans.

## **Database Preview**
Below is a sample preview of the MongoDB collection used for storing scraped data:

![Database Preview](path/to/your/image.png)
