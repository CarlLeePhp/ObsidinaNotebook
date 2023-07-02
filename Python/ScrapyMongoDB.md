## Installation

We need the Scrapy library along with PyMongo for storing the data in MongoDB.

```shell
sudo apt-get install python3-dev build-essential

pip install Scrapy
```



### Tutorial

1. Creating a new Scrapy Project;
2. Writing a spider to crawl a site and extract data;
3. Exporting the scraped data using the command line;
4. Changing spider to recursively follow links;
5. Using spider arguments.



```shell
# Creating a project
scrapy startproject tutorial
cd turorial

# config before running
# run
scrapy crawl quotes
```







## Reference

https://realpython.com/web-scraping-with-scrapy-and-mongodb/

https://docs.scrapy.org/en/latest/index.html