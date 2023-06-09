# 律水清山平台

软工导论第4小组的开发项目，项目文件包括需求分析文档，系统设计文档，项目源代码，系统测试文档，部分功能使用了文本挖掘算法与深度学习模型。

### 开发环境

- 开发语言： 后端 - Java(jdk1.8)，Python(3.7)，前端 - Html
- 使用框架：Spring Boot(2.1.3)，MyBatis，Junit，pytorch(1.4)
- 数据库：mysql(8.0)
- 项目管理：Maven
- IDE：JetBrains Intelij IDEA 2021
- 开发系统：Windows10
- 网络服务器：Tomcat(9.0)
- 客户端浏览器：尽量使用Google Chrome，目前已知IE浏览器会出现前端格式错误的问题


### 代码结构

```
legalsys
├─src 
│	├─main
│		├─java
│			├─com.huidong.legalsys
│				├─aspect（权限管理）
│					├─LoginAspect.java
│				├─configuration
│					├─DataSourceConfiguration.java
│					├─UploadFileConfiguration.java
│				├─controller（业务表现层）
│					├─ConsultController.java
│					├─LoginController.java
│					├─ManageController.java
│					├─PenallawController.java
│					├─SessionController.java
│					├─StatisticsController.java
│				├─dao（数据访问层）
│					├─ConsultDao.java
│					├─ConvrDao.java
│					├─LoginDao.java
│					├─SessionDao.java
│					├─StatureDao.java
│					├─UserDao.java
│				├─domain（实体层）
│					├─Consult.java
│					├─Convr.java
│					├─ConvrContent.java
│					├─Error.java
│					├─Login.java
│					├─Session.java
│					├─Stature.java
│					├─User.java
│				├─enumeration
│					├─ConsultTypeEnum.java
│					├─ErrorEnum.java
│					├─LoginStatusEnum.java
│					├─RegisterTypeEnum.java
│					├─SessionStatusEnum.java
│				├─exception
│					├─LegalsysException.java
│				├─handle
│					├─ExceptionHandle.java
│				├─listener（在线人数监听）
│					├─HttpSessionListener.java
│					├─RequestContextListener.java
│					├─ServletContextListener.java
│				├─service（业务逻辑层）
│					├─ConsultService.java
│					├─LoginService.java
│					├─ManageService.java
│					├─PenallawService.java
│					├─SessionService.java
│					├─StatisticsService.java
│					├─UploadService.java
│				├─util
│					├─ErrorUtil.java
│				├─LegalsysApplication.java（项目启动类）
│		├─resources
│			├─mapper（Mybatis映射）
│				├─ConsultMapper.xml
│				├─ConvrMapper.xml
│				├─LoginMapper.xml
│				├─SessionMapper.xml
│				├─StatureMapper.xml
│				├─UserMapper.xml
│			├─python
│				├─model（存放深度学习模型）
│				├─preprocess.py
│				├─predictor.py
│			├─static
│				├─css
│					├─fonts
│					├─style.css（html配置文件）
│				├─images（存放图片文件）
│				├─stature（存放刑法数据）
│			├─templates（html文件）
│			├─application.yml（配置文件）
│			├─application.properties（配置文件）
│		├─resourcesupload（律师执照上传路径）
├─test（单元测试的一些代码，写的比较乱，所以部署的时候没放在src目录下）
├─init.sql（mysql新建数据库及表单）
├─pom.xml（Maven项目配置文件）
```

### 项目部署

1. - 安装MySQL Community Server，https://dev.mysql.com/downloads/mysql/

2. - cd legalsys目录
   - 运行mysql -u root -p，输入密码
   - 运行source init.sql建立数据库，初始化表单

3. - 安装JetBrains IntelliJ IDEA Ultimate，https://www.jetbrains.com/idea/download/#section=windows
   - 可以申请教育版，https://www.jetbrains.com/community/education/#students

4. - 下载安装Maven，http://maven.apache.org/index.html
   - 配置镜像，本地仓库

5. - IDEA中打开legalsys项目文件
   - 右键点击pom.xml，点击Maven，点击Reimport
6. - 修改项目的名字问legalsys
   - 设置Spring Boot Configuration ：
   - 点击Edit Configuration，从模板Templates新建Spring Boot，Main class选择com.huidong.legalsys.LegalsysApplication，Use classpath of modules选择legalsys文件夹
   - 设置Tomcat Configuration：
   - 从模板Templates新建Tomcat Local
   - 找到File - Project Structure - Project Settings - Artifacts，新建legelsys:war exploded
   - 在刚才新建的Tomcat Local，Before launch中添加刚才新建的legelsys:war exploded artifact
   - 添加Mysql数据库连接，输入用户名root，密码******，数据库名称legalsys
   - maven clean install 部署项目
   
7. - 安装python3，pytorch1.4环境，推荐通过[anaconda](https://www.anaconda.com/products/individual)配置
   - 添加anaconda环境变量
   - cmd运行cd legalsys根目录/src/main/resources/python
   - 运行conda activate (你配置的pytorch1.4环境名)
   - 运行python predictor.py启动深度学习模型计算的服务

   
- 开发之前没有相关经验，所有东西都是现学现卖，所以对spring boot的底层逻辑不清楚，前端开发的方法也不了解。虽然项目简单，但是代码中肯定有诸多不正确的地方，恳请大家能够包容，欢迎批评指正。

