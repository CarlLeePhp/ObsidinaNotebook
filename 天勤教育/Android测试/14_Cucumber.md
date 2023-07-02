## BDD Framework

#### 实现步骤

安装依赖支持，Runner 换成 Cucumber Runner。

**Steps:**

1. Write User Behaviours in feature file.
2. Copy the step definitions.
3. Implement the step definitions.
4. Config the Cucumber options.



#### Reference

http://cucumber.io/docs/installation/android/



## Web Server Mock

#### 实现步骤

安装依赖支持；更改源程序 ；创建假资源 (json)；创建 Mock。

#### Why Mock

What if API is not ready? What if the testing server is down? What if the API response you want to acquire is hard to get? such as: you have to get certificate, token, or some other preconditions. What if the API response you want connot be acquired from Server, such as: current time?



+ Firstly, do not have to wait the API development completed. Could be developed at the same time.



https://www.confluent.io/blog/choosing-between-mock-api-and-real-backend/

Here are some advantages to using API mocks in your development workflow:

+ You can do feature work even if your external dependencies are unavailable.
+ Mock API frameworks are generally quite flexible. They can be programmed to programmed to emulate almost any external API.
+ Because they are lightweight, mock servers are quick to iterate on, requiring much less time to redeploy changes than an actual dev backend.
+ Mock servers are often stateless, which makes repeatedly testing the same scenarios very easy.



**Testing should be done in a hermetic 封闭的 environment**

no dependency on external environment, such as: server, database etc.

**Testing should always produce consistent results.**

Repeatable tests should have reliable results.



#### Reference

http://wiremock.org/



