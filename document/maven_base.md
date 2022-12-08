# Maven_Base

# 1. 为什么要使用Maven

## 1.1 获取jar包

​	使用Maven之前，自行在网络中下载jar包，效率较低，如【谷歌、百度、CSDN....】

​	使用Maven之后，统一在一个地址下载资源jar包【阿里云镜像服务器等...】

## 1.2 添加jar包

​	使用Maven之前，将jar复制到项目工程中，jar包添加到项目中，相对浪费存储空间

​	使用Maven之后，jar包统一存储Maven本地仓库，使用坐标方式将jar包从仓库引入到项目中

​	使用Maven便于解决jar包**冲突及依赖**问题

​	![image-20221124144838710](assets\image-20221124144838710.png)

# 2. 什么是Maven

​		**Maven**是**Apache**的一个项目管理工具，主要作用是在项目开发阶段对Java项目进行**依赖管理**和**项目构建**

​		**官网下载：**http://maven.apache.org/

​		**查找依赖：**https://mvnrepository.com/

​		**Maven底层：**Maven底层是采使用Java语言编写的，所以**安装Maven**时需要配置**JAVA_HOME**环境变量及**Path**

​		**安装注意：**将Maven解压**非中文无空格**目录下，所以以前安装**JDK目录**也建议安装到非中文无空格目录下，

​							后面的**tomcat**应用服务器安装目录也是要解压到非中文无空格目录下！

​		**配置环境变量：**配置**MAVEN_HOME**环境变量及Path

​		**检测Maven环境是否搭建成功：**输入**cmd**,进入命令行窗口，输入**mvn -v** ，检查Maven环境是否搭建成功

## 2.1 依赖管理

​		**依赖管理**就是对**jar包**的管理，通过导入**maven坐标**，就相当于将仓库中的jar包导入了当前项目中

## 2.2 项目构建

​		**项目构建**就是通过**maven**的一个命令就可以完成项目从清理、编译、测试、报告、打包，部署整个过程

# 3. maven主要功能

 - 提供了一套标准化的项目结构
 - 提供了一套标准化的构建流程（编译，测试，打包，发布……）
 - 提供了一套依赖管理机制

# 4. maven 作用

- 标准化的项目结构

  ![image-20221124150642529](assets\image-20221124150642529.png)

- 标准化的构建流程

  ![image-20221124150840788](assets\image-20221124150840788.png)

- 方便的依赖管理

![image-20221124150814831](assets\image-20221124150814831.png)

# 5. Maven 模型

- 项目对象模型 (Project Object Model)
- 依赖管理模型(Dependency)
- 插件(Plugin)

![image-20221030180123177](assets\image-20221030180123177.png)

# 6. Maven仓库分类

## 6.1 本地仓库

​	本地仓库就是自己计算机上的一个目录（Git分布式版本系统，也分本地仓库，远程仓库）

## 6.2 中央仓库

​	中央仓库就是由Maven团队维护的全球唯一的仓库

​	地址：https://repo1.maven.org/maven2/

## 6.3 远程仓库（私服）

​		远程仓库又称私服，一般由公司团队搭建的私有仓库！

# 7. Maven仓库查找依赖规则

​	当项目中使用坐标引入对应依赖jar包后，首先会查找本地仓库中是否有对应的jar包，

​	如果有，则在项目直接引用，如果没有，则去中央仓库中下载对应的jar包到本地仓库，即 本地仓库 -> 中央仓库

​	除此之外还可以搭建远程仓库，远程仓库搭建完毕，jar包的查找顺序则变为：本地仓库 -> 远程仓库 -> 中央仓库

![image-20221030180655334](assets\image-20221030180655334.png)

# 8. Maven 基本配置顺序

 - 1. 解压 apache-maven-3.6.1.rar 既安装完成

 - 2. 配置环境变量 MAVEN_HOME 为安装路径的bin目录

 - 3. 配置本地仓库：修改 conf/settings.xml 中的 <localRepository> 为一个指定目录

      Maven配置文件位置：maven根目录/conf/settings.xml

      自定义本地仓库【默认本地仓库：C:/用户家目录/.m2/repository】

      ![image-20221124152101017](assets\image-20221124152101017.png)

 - 4. maven 配置阿里云私服：修改 conf/settings.xml 中的 <mirrors>标签，为其添加如下子标签：

      ![image-20221124163944063](assets\image-20221124163944063.png)

```
<mirror> 
	<id>alimaven</id>
	<name>aliyun maven</name>
	<url>http://maven.aliyun.com/nexus/content/groups/public/</url>
	<mirrorOf>central</mirrorOf>
</mirror>
```

**为什么配置阿里云私服器？**

​	因为中央仓库在国外，下载比较慢，所以可以配置为定向到阿里云镜像【国外调到国内，访问速度就相比较快了些】，

​	还有，阿里云镜像里面一般都很全！

**镜像是什么？**

​	镜像是一种文件存储形式，是冗余的一种类型，一个磁盘上的数据在另一个磁盘上存在一个完全相同的副本即为镜像！

- 5. 设置使用JDK版本【1.8|JDK8】

  ```
  <profiles>
  	<profile>
        <id>jdk-1.8</id>
        <activation>
          <activeByDefault>true</activeByDefault>
          <jdk>1.8</jdk>
        </activation>
        <properties>
          <maven.compiler.source>1.8</maven.compiler.source>
          <maven.compiler.target>1.8</maven.compiler.target>
          <maven.compiler.compilerVersion>1.8</maven.compiler.compilerVersion>
        </properties>
      </profile>
  </profiles>
  ```

# 9. Maven 常用命令

- compile ：编译
- clean：清理
- test：测试
- package：打包
- install：安装

# 10. Maven 生命周期

​	Maven 对项目构建的生命周期划分为3套

​	**1. clean：**清理工作

​	**2. default：**核心工作，例如编译，测试，打包，安装等

​	**3. site：**产生报告，发布站点等

​	**注意：**同一生命周期内，执行后边的命令，前边的所有命令会自动执行

​	**例如：** install执行，前面的 comiple、test、package 都会自动执行，表现出的是一连贯动作！

![image-20221030181220701](assets\image-20221030181220701.png)

# 11. default 构建生命周期

![image-20221030181257079](assets\image-20221030181257079.png)

# 12. IDEA 配置 Maven

- 1. 选择 IDEA中 File --> Settings

     ![image-20221124154910363](assets\image-20221124154910363.png)

- 2. 搜索 maven

     ![image-20221124154927518](assets\image-20221124154927518.png)

- 3. 设置 IDEA 使用本地安装的 Maven，并修改配置文件路径

![image-20221030181552227](assets\image-20221030181552227.png)

# 13. Maven 坐标详解

## 13.1 什么是坐标？

​		Maven 中的坐标是资源的唯一标识

​		使用坐标来定义项目或引入项目中需要的依赖

## 13.2 Maven 坐标主要组成

​		**groupId：**定义当前Maven项目隶属组织名称（通常是域名反写，例如：com.yj.nz）

​		**artifactId：**定义当前Maven项目名称（通常是模块名称，例如 order-service、goods-service）

​		**version：**定义当前项目版本号

![image-20221124155352244](assets\image-20221124155352244.png)

![image-20221124155415366](assets\image-20221124155415366.png)

# 14. IDEA创建Maven项目

- 1. 创建模块，选择Maven，点击Next

- 2. 填写模块名称，坐标信息，点击finish，创建完成

- 3. 编写 HelloWorld，并运行

  ![image-20221124155716439](assets\image-20221124155716439.png)

![image-20221124155957940](assets\image-20221124155957940.png)

# 15. IDEA 导入 Maven 项目

- 1. 选择右侧Maven面板，点击 + 号
- 2. 选中对应项目的pom.xml文件，双击即可
- 3. 如果没有Maven面板，选择
       View -> Appearance -> Tool Window Bars

![image-20221030182244589](assets\image-20221030182244589.png)

![image-20221030182321167](assets\image-20221030182321167.png)

![image-20221030182328244](assets\image-20221030182328244.png)

# 16. 配置 Maven-Helper 插件

- 1. 选择 IDEA中 File --> Settings
- 2. 选择 Plugins
- 3. 搜索 Maven，选择第一个 Maven Helper，点击Install安装，弹出面板中点击Accept
- 4. 重启 IDEA

![image-20221030182443167](assets\image-20221030182443167.png)

![image-20221030182459573](assets\image-20221030182459573.png)

![image-20221030182520897](assets\image-20221030182520897.png)

![image-20221030182534170](assets\image-20221030182534170.png)

# 17. 依赖管理

​	**使用坐标导入 jar 包 步骤**
- 1. 在 pom.xml 中编写 <dependencies> 标签
- 2. 在 <dependencies> 标签中 使用 <dependency> 引入坐标
- 3. 定义坐标的 groupId，artifactId，version
- 4. 点击刷新按钮，使坐标生效

![image-20221030182623236](assets\image-20221030182623236.png)

![image-20221030182627678](assets\image-20221030182627678.png)

​	**使用坐标导入 jar 包 – 快捷方式**

- 1. 在 pom.xml 中 按 alt + insert，选择 Dependency
- 2. 在弹出的面板中搜索对应坐标，然后双击选中对应坐标
- 3. 点击刷新按钮，使坐标生效

![image-20221030182812560](assets\image-20221030182812560.png)

![image-20221030182824038](assets\image-20221030182824038.png)

![image-20221030182839814](assets\image-20221030182839814.png)

​	**使用坐标导入 jar 包 – 自动导入**
- 1. 选择 IDEA中 File --> Settings
- 2. 在弹出的面板中找到 Build Tools
- 3. 选择 Any changes，点击 ok 即可生效

![image-20221030182916645](assets\image-20221030182916645.png)

![image-20221030182927688](assets\image-20221030182927688.png)

# 18. 依赖范围

​	通过设置坐标的依赖范围(scope)，可以设置 对应jar包的作用范围：编译环境、测试环境、运行环境
​	**<scope>默认值：**compile

![image-20221030183045220](assets\image-20221030183045220.png)

![image-20221030183053406](assets\image-20221030183053406.png)

