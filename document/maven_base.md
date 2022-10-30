# 五、maven_base

# 1. Maven简介

```
1. maven是什么
	Apache Maven是一个项目管理工具，主要作用是在项目开发阶段对Java项目进行依赖管理和项目构建
	官网：http://maven.apache.org/
	查找依赖：https://mvnrepository.com/
	1、依赖管理：
		就是对jar包的管理，通过导入maven坐标，就相当于将仓库中的jar包导入了当前项目中
	2、项目构建：
		通过maven的一个命令就可以完成项目从清理、编译、测试、报告、打包，部署整个过程
		
2. maven主要工功能
	1、提供了一套标准化的项目结构
	2、提供了一套标准化的构建流程（编译，测试，打包，发布……）
	3、提供了一套依赖管理机制
3. maven作用
	1、标准化的项目结构
	2、标准化的构建流程
	3、方便的依赖管理
```

## 	1. 标准化的项目结构

![image-20221030173607146](assets\image-20221030173607146.png)

## 	2. 标准化的构建流程

![image-20221030173736129](assets\image-20221030173736129.png)

## 	3. 依赖管理

# ![image-20221030175639568](assets\image-20221030175639568.png)2. Maven 模型

```
1. 项目对象模型 (Project Object Model)
2. 依赖管理模型(Dependency)
3. 插件(Plugin)
```

![image-20221030180123177](assets\image-20221030180123177.png)

# 3. Maven仓库分类

```
1. 本地仓库
	自己计算机上的一个目录
2. 中央仓库
	由Maven团队维护的全球唯一的仓库
	地址：https://repo1.maven.org/maven2/
3. 远程仓库(私服)
	一般由公司团队搭建的私有仓库
	
当项目中使用坐标引入对应依赖jar包后，首先会查找本地仓库中是否有对应的jar包
	如果有，则在项目直接引用;
	如果没有，则去中央仓库中下载对应的jar包到本地仓库

还可以搭建远程仓库，将来jar包的查找顺序则变为
	本地仓库 -> 远程仓库 -> 中央仓库
```

![image-20221030180655334](assets\image-20221030180655334.png)

# 4. Maven 安装配置

```
1. 解压 apache-maven-3.6.1.rar 既安装完成
2. 配置环境变量 MAVEN_HOME 为安装路径的bin目录
3. 配置本地仓库：修改 conf/settings.xml 中的 <localRepository> 为一个指定目录
4. 配置阿里云私服：修改 conf/settings.xml 中的 <mirrors>标签，为其添加如下子标签：
<mirror>  
	<id>alimaven</id>  
	<name>aliyun maven</name>  
	<url>http://maven.aliyun.com/nexus/content/groups/public/</url>
	<mirrorOf>central</mirrorOf>          
</mirror>
```

# 5. Maven 常用命令

```
compile ：编译
clean：清理
test：测试
package：打包
install：安装
```

# 6. Maven 生命周期

```
Maven 构建项目生命周期描述的是一次构建过程经历经历了多少个事件
Maven 对项目构建的生命周期划分为3套
	clean：清理工作
	default：核心工作，例如编译，测试，打包，安装等
	site：产生报告，发布站点等
同一生命周期内，执行后边的命令，前边的所有命令会自动执行
```

![image-20221030181220701](assets\image-20221030181220701.png)

# 7. default 构建生命周期

![image-20221030181257079](assets\image-20221030181257079.png)

# 8. IDEA 配置 Maven

```
1. 选择 IDEA中 File --> Settings

2. 搜索 maven

3. 设置 IDEA 使用本地安装的 Maven，并修改配置文件路径
```

![image-20221030181521338](assets\image-20221030181521338.png)

![image-20221030181544654](assets\image-20221030181544654.png)

![image-20221030181552227](assets\image-20221030181552227.png)

# 9. Maven 坐标详解

```
1. 什么是坐标？
	Maven 中的坐标是资源的唯一标识
	使用坐标来定义项目或引入项目中需要的依赖
2. Maven 坐标主要组成
	groupId：定义当前Maven项目隶属组织名称（通常是域名反写，例如：com.itheima）
	artifactId：定义当前Maven项目名称（通常是模块名称，例如 order-service、goods-service）
	version：定义当前项目版本号
```

![image-20221030182040109](assets\image-20221030182040109.png)

# 10. IDEA创建Maven项目

```
1. 创建模块，选择Maven，点击Next
2. 填写模块名称，坐标信息，点击finish，创建完成
3. 编写 HelloWorld，并运行
```

![image-20221030182135040](assets\image-20221030182135040.png)

![image-20221030182140818](assets\image-20221030182140818.png)

# 11. IDEA 导入 Maven 项目

```
1. 选择右侧Maven面板，点击 + 号
2. 选中对应项目的pom.xml文件，双击即可
3. 如果没有Maven面板，选择
    View -> Appearance -> Tool Window Bars
```

![image-20221030182244589](assets\image-20221030182244589.png)

![image-20221030182321167](assets\image-20221030182321167.png)

![image-20221030182328244](assets\image-20221030182328244.png)

# 12. 配置 Maven-Helper 插件

```
1. 选择 IDEA中 File --> Settings
2. 选择 Plugins
3. 搜索 Maven，选择第一个 Maven Helper，点击Install安装，弹出面板中点击Accept
4. 重启 IDEA
```

![image-20221030182443167](assets\image-20221030182443167.png)

![image-20221030182459573](assets\image-20221030182459573.png)

![image-20221030182520897](assets\image-20221030182520897.png)

![image-20221030182534170](assets\image-20221030182534170.png)

# 13. 依赖管理

```
使用坐标导入 jar 包 步骤
1. 在 pom.xml 中编写 <dependencies> 标签
2. 在 <dependencies> 标签中 使用 <dependency> 引入坐标
3. 定义坐标的 groupId，artifactId，version
4. 点击刷新按钮，使坐标生效
```

![image-20221030182623236](assets\image-20221030182623236.png)

![image-20221030182627678](assets\image-20221030182627678.png)

```
使用坐标导入 jar 包 – 快捷方式
1. 在 pom.xml 中 按 alt + insert，选择 Dependency
2. 在弹出的面板中搜索对应坐标，然后双击选中对应坐标
3. 点击刷新按钮，使坐标生效
```

![image-20221030182812560](assets\image-20221030182812560.png)

![image-20221030182824038](assets\image-20221030182824038.png)

![image-20221030182839814](assets\image-20221030182839814.png)

```
使用坐标导入 jar 包 – 自动导入
1. 选择 IDEA中 File --> Settings
2. 在弹出的面板中找到 Build Tools
3. 选择 Any changes，点击 ok 即可生效
```

![image-20221030182916645](assets\image-20221030182916645.png)

![image-20221030182927688](assets\image-20221030182927688.png)

# 14. 依赖范围

```
通过设置坐标的依赖范围(scope)，可以设置 对应jar包的作用范围：编译环境、测试环境、运行环境
<scope>默认值：compile
```

![image-20221030183045220](assets\image-20221030183045220.png)

![image-20221030183053406](assets\image-20221030183053406.png)
