参考《精通 Python 爬虫框架 Scrapy》第二章

使用 * 来选择指定层级的所有元素，比如：

$x('//div/*')



#### 第 3 章 爬虫基础

所有 IT 工作的搜索链接：https://www.seek.co.nz/jobs-in-information-communication-technology

| 基本字段         | XPath 表达式                               |
| ---------------- | ------------------------------------------ |
| 工作 / title     | //*[@data-automation="jobTitle"]/text()    |
| 公司名 / company | //*[@data-automation="jobCompany"]/text()  |
| 地点 / location  | //*[@data-automation="jobLocation"]/text() |
|                  |                                            |
|                  |                                            |



**创建项目和爬虫**

```shell
# Create a project
$ scrapy startproject projectName

# Create a spider
$ scrapy genspider basic web

# Run a spider
$ scrapy crawl basic
```

