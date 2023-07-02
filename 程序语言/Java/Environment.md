### 下载解压和环境配置

比如解压到 /usr/java/, tar zxvf xxx.tar.gz;

环境配置，家目录下 .bashrc 末尾添加

```shell
export JAVA_HOME=/usr/java/jdk1.7.0_40
export JRE_HOME=$JAVA_HOME/jre
export CLASSPATH=.:$JAVA_HOME/lib:$JRE_HOME/lib
export PATH=$JAVA_HOME/bin:$JRE_HOME/bin:$PATH
```

检查版本：java -version

切换版本：

sudo update-alternatives --config java

### PPA 安装

```shell
# Add the PPA
sudo add-apt-repository ppa:webupd8team/java

# Install
sudo apt update
sudo apt install oracle-java8-installer
```

### IntelliJ

+ Don't import settings
+ Config > Project Default > Project Structure
+ New ... > JDK > [Find your JDK]

**Make it easy to study Java**

+ Settings > Editor > General > Auto Import > Check the two below:
  + Add unambiguous imports on the fly
  + Optimize imports on the fly (for current project)
+ ... > General > Apperance > Check the "Line Number"
+ ... > General > Code Folding > Uncheck belows:
  + Imports
  + One-Line Methods
  + "Closures"
  + Generic constructor and ...

### Maven

Homepage: https://maven.apache.org

可以下载二进制包

环境配置，家目录下 .bashrc 添加

```shell
export PATH=~/opt/apache-maven-3.5.3/bin:$PATH
```

用 mvn -v 检查版本。

#### Make a simplest project

```shell
mvn archetype:generate \
	-DarchetypeGroupId=org.apahce.maven.archetypes \
	-DgroupId=com.mycompany.app \
	-DartifactId=my-app
```

The src/main/java directory contains the project source code, the src/test/java directory contains the test source, and the pom.xml file is the project's Project Object Model, or POM.



#### Building and Testing

```shell
mvn clean package
```

+ 首先清理目标文件，然后打包项目构建的输出为 jar 文件。
+ 打包好的文件在 target\
+ 测试报告存放在 target\surefire-reports\
+ 编译源码，以及测试源码；
+ 接着 Maven 运行测试用例；
+ 最后 Maven 创建项目包。





#### Benifits with Maven

