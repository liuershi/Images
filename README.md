# Streamer FT web 文档说明

##  一、技术选择

1.1、**使用工具**

- IDEA，GitLab进行项目版本管理
- 禅道进行问题提出，bug汇总以及解决
- 测试服务器：Linux centos 7

1.2、**项目技术**

1. springboot+angularJS，整体为B/S架构
2. 注解@Controller配置Controller层，注解@Service实现Service层和Service接口的实现层，通过Socket与服务端通信实现Dao层
3. SpringBoot+Jquery+angularJS+html完成前端页面展示
4. 使用ajax回调获取后台数据后使用JavaScript+HTML+css+Echarts+bootstrap table等技术进行展示
5. lombok简化实体类的代码
6. 通过socket基于protobuf协议与服务端（c语言实现）通信

## 二、功能模块

按照页面布局可分为下列八大模块：

1. 登录模块：包括登录注销授权等功能
2. 存储资源模块：主要对磁盘以及存储空间的curl操作
3. 客户端模块：系统主要模块，磁盘的备份数据同步与恢复等重要功能
4. 文件备份模块：文件备份客户端备份计划的创建以及恢复任务的执行
5. 应急接管模块：对streamer的全量与增量恢复以及vnc的实现
6. 容灾配置模块：包括荣在服务器与客户端，主要是对客户端的容灾关系操作
7. 系统日志模块：操作日志的记录，也包括日志的下载
8. 系统设置模块：包括用户的curl，密码设置网络配置以及streamer宿主机的管理

## 三、项目目录说明

#### 1、项目整体结构

父模块为streamer-interface-web-service，包含三个子模块，分别为streamer-interface-web-service-api、streamer-interface-web-service-client、streamer-interface-web-service-core

```java
streamer-interface-web-service
    .idea
    .settings
    classes
    streamer-interface-web-service-api
    streamer-interface-web-service-client
    streamer-interface-web-service-core
    .gitignore
    .project
    hs_err_pid137356.log
    pom.xml
    streamer-interface-web-service-parent.iml
```

#### 2、父模块

主要作用是提供子模块的公共依赖：

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
		 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
		 xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<groupId>cn.infocore</groupId>
	<artifactId>streamer-interface-web-service-parent</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<packaging>pom</packaging>
	<name>streamer-interface-web-service-parent</name>
	<properties>
		<springfox.version>2.9.2</springfox.version>
		<java.version>1.8</java.version>
		<maven.compiler.target>1.8</maven.compiler.target>
		<maven.compiler.source>1.8</maven.compiler.source>
		<springboot.version>2.1.1.RELEASE</springboot.version>
		<spring-platform.version>Cairo-RELEASE</spring-platform.version>
		<lombok.version>1.16.18</lombok.version>
		<spring-cloud.version>Greenwich.SR2</spring-cloud.version>
		<edas.version>1.0.2</edas.version>
		<jwt.version>3.8.0</jwt.version>
		<dubbo.version>2.7.0</dubbo.version>
		<dubbo.registry.nacos.version>0.0.2</dubbo.registry.nacos.version>
		<seata.version>0.7.1</seata.version>
		<nacos.version>0.9.0.RELEASE</nacos.version>
		<mybatis-plus.version>3.1.2</mybatis-plus.version>
		<mybatis.version>2.0.1</mybatis.version>
		<pagehelper.version>1.2.10</pagehelper.version>
		<swagger.version>1.5.13</swagger.version>
		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
	</properties>
	<modules>
		<module>streamer-interface-web-service-api</module>
		<module>streamer-interface-web-service-client</module>
		<module>streamer-interface-web-service-core</module>
	</modules>
	<dependencyManagement>


		<dependencies>
			<dependency>
				<groupId>org.springframework.cloud</groupId>
				<artifactId>spring-cloud-dependencies</artifactId>
				<version>${spring-cloud.version}</version>
				<type>pom</type>
				<scope>import</scope>
			</dependency>
			<dependency>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-dependencies</artifactId>
				<version>${springboot.version}</version>
				<type>pom</type>
				<scope>import</scope>
			</dependency>
			<dependency>
				<groupId>io.spring.platform</groupId>
				<artifactId>platform-bom</artifactId>
				<version>${spring-platform.version}</version>
				<type>pom</type>
				<scope>import</scope>
			</dependency>

			<dependency>
				<groupId>com.fasterxml.jackson.core</groupId>
				<artifactId>jackson-databind</artifactId>
				<version>2.9.9.3</version>
			</dependency>
			<dependency>
				<groupId>com.googlecode.protobuf-java-format</groupId>
				<artifactId>protobuf-java-format</artifactId>
				<version>1.2</version>
			</dependency>

			<!-- https://mvnrepository.com/artifact/junit/junit -->
			<dependency>
				<groupId>junit</groupId>
				<artifactId>junit</artifactId>
				<version>4.12</version>
				<scope>test</scope>
			</dependency>
			<dependency>
				<groupId>io.netty</groupId>
				<artifactId>netty-all</artifactId>
				<version>4.1.39.Final</version>
			</dependency>
		</dependencies>
	</dependencyManagement>

	<dependencies>
		<dependency>
			<groupId>org.projectlombok</groupId>
			<artifactId>lombok</artifactId>
		</dependency>
	</dependencies>
	<build>
		<plugins>
			<plugin>
				<artifactId>maven-compiler-plugin</artifactId>
				<version>3.8.1</version>
				<configuration>
					<fork>true</fork>
					<executable>
						C:\Program Files (x86)\Java\jdk1.8.0_231\bin\javac.exe
					</executable>
				</configuration>
			</plugin>
		</plugins>
	</build>
</project>
```



#### 3、子模块

总共包含三个子模块

1. streamer-interface-web-service-api

   主要存放protobuf协议对应的Java bean

   目录结构：

   ```java
   src
   	main
   		java
       		cn.infocore
   				bean
   				common
   				exceptions
   				protobuf
   				streamer_console.proto
   		resources
   ```

   其中，bean包中包含的是有特殊功能要求被protobuf转换成的普通java bean；common中包含的是java后端返回给前端的java定义类，类似前后端的自定义协议；exceptions中包含一个自定义的异常类；protobuf中包含的protobuf协议转换成的java类；streamer_console.proto就是协议文件。  

2. streamer-interface-web-service-client

   包括MVC层，主要是接收前端请求请求与响应

   目录结构

   ```java
   src
   	main
   		java
   			cn.infocore
       			bean							--需要将protobuf转换成普通的java bean
   				controller						--处理请求的所有controller
   				dto								--文件备份模块中任务计划的一个实体类
   				exception						--自定义异常
   				ServerSocket					--与服务端通信的socket处理
   				service							--所有的service以及service实现层
   				utils							--自定义的一些公用操作
   				StreamerWebServiceApplication	--springboot启动类
   		resources			
       		static								--其中包含的所有文件都是前端工程文件，根据不同的功能分类，每个文件夹中都包含对应的HTML页面与js文件
       			clients							--客户端模块
       			css								--css样式
       			dr								--容灾配置模块
       			files							--文件备份模块
       			images							--前端页面显示的图片
       			js								--接收文件，包括bootstrap与jQuery等等
       			kvm								--应急接管模块
       			license							--授权模块
       			login							--登录模块
       			logs							--系统日志模块
       			node_modules					--自定义的js处理文件以及其他插件，包括angularJS等等
       			overview						--存储资源中存储资源使用请求显示模块
       			settings						--系统设置模块
       			storage-resources				--存储资源模块
       			app.js							--全局的js文件，定义了工程所需的依赖，封装了所有的请求发送与处理逻辑包括未登录请求的重定向等等。
       			default.html					--默认加载页面
       			favicon.ico						--网页图标
       			index.html						--重定向转向的页面
       			main.js							--定义所有模块的依赖，包括bootstrap与angularJS
       			package.json					--定义了项目的各种模块以及配置信息
       	application.properties					--springboot项目配置文件
   ```

3. streamer-interface-web-service-core

   主要是存储用户信息

   目录

   ```xml
   src
   	main
   		java
   			cn.infocore
   				bean							--包含存储用户信息
   				common							--定义与服务端处理的协议类以及socket通信的通用模块等等
   				config							--定义拦截器与过滤器处理登陆请求以及跨域
   				core							--定义全局异常处理类以protobuf生成类转换成普通java bean的转换器
   				service							--文件下载的处理类
   ```

#### 4、处理流程说明

- ​	前端

  根据不同的功能分成不同的模块，具体的模块有对应的module.js以及service.js，这两个文件分别作用是定义当前模块各组件的路由配置和定义当前模块中个请求的定义，我么在加载该模块时首先会加载module.js，以系统日志模块为例：

  当我们点击系统日志模块时，即下图

  ![](https://github.com/liuershi/Images/raw/master/1580905928(1).jpg?raw=true)

  根据对应的index.html我们可得知

  ```html
  <li ui-sref-active="{'active':'home.logs'}" role="presentation">
      <a href="javascript:void(0);" ui-sref="home.logs">
          <img class="normal" alt="" src="images/syslog_menu.png" width="20px">
          <img class="active" alt="" src="images/syslog_menu.png" width="20px">
          <span style="padding-left: 10px;vertical-align: middle;"> 系统日志</span>
      </a>
  </li>
  ```

  此时会路由到home.logs路径下，home代表的是根目录即static，它会去加载logs目录文件，而且是加载module.js文件，我们看module.js文件的结构。

  module.js：

  ```js
  //各个模块的路由对anuglar模块的依赖是必须的，因为这种依赖关系不能在shim中配置，只能在此依赖
  define(['angular'],function(){
  	var logsModule=angular.module('logs',[]);
  	logsModule.config(['$stateProvider',function($stateProvider){
  		$stateProvider.state({
  			name:'home.logs',
  			url:'/logs?{type:int}',
  			params:{
  				'type':{value:0}
  			},
  			component:'logsIndex',
  			onExit:['$rootScope','$interval',function($rootScope,$interval){
  				if($rootScope.getCompressLogStatusInterval){
  					$interval.cancel($rootScope.getCompressLogStatusInterval);
  					$rootScope.getCompressLogStatusInterval=null;
  				}
  			}],
  			lazyLoad: function($transition$){
  				//加载对应的组件
  				return $transition$.injector().get('$ocLazyLoad').load(['logs/service','logs/index/component']);
  			}
  		});
  	}]);
  });
  ```

  定义一个名为logs的模块，给它配置加载的模块路径为"home.logs"，此时home是指当前根目录下，即static下，url为路由的路径，params指定义名为type的参数，值默认为0，component指加载名为logsIndex的js文件，而onExit是指当退出此模块时执行定义的function，而lazyload则是加载指定路径下的文件，例子中是加载'logs/service'，'logs/index/component'的文件，分别看这两个文件。

  service.js：

  ```js
  define(['angular'],function(){
  	angular.module('logs').factory('logsService',['$resource','basePath',function($resource,basePath){
  		return $resource(basePath+'/log',{},{
  			'getLogSelect' : {
  				url:basePath+'/log/logSelect',
  				method:'post'
  			},
  			'getLog' : {
  				url:basePath+'/log/logGet',
  				method:'post'
  			},
  			'getCompressedLogList' : {
  				url:basePath+'/log/getCompressedLogList',
  				method:'get'
  			},
  			'addCompressLog' : {
  				url:basePath+'/log/compressLog',
  				method:'post'
  			},
  			'getCompreddLogStatus' : {
  				url:basePath+'/log/getCompressLogStatus',
  				method:'get'
  			},
  			'getLogExport' : {
  				url:basePath+'/log/logExport',
  				method:'post'
  			},
  			'getClientsInfo' : {
  				url:basePath+'/client/getClientsInfo',
  				method:'get'
  			},
  			'getCompressLogStatus':{
  				url:basePath+'/log/getCompressLogStatus',
  				method:'get'
  			}
  		});
  	}]);
  });
  ```

  根据我们之前定义的logs模块创建名为logsService的指令集，该指令集中定义了我们在该模块中所需要的的所有的请求，每个请求的格式为请求名后面接请求体，请求体中的url为我们后端定义的接收请求的url，method为请求类型，本项目中全为get与post，请求类型根据具体请求功能区分类型，它的作用主要就是定义日志模块中的全部请求。

  由module.js中我们可知此时会路由到logs/index下的component.js文件，该文件的结构如下：

  ```js
  angular.module('logs').component('logsIndex',{
  	templateUrl:'logs/index/template.html?'+resourcesVersion,
  	controller:[
  		'utils',
  		'logsService',
  		'NgTableParams',
  		'$state',
  		'$window',
  		'$scope',
  		'$rootElement',
  		'$element',
  		'$compile',
  		'$rootScope',
  		'$q',
  		'$interval',function(
  				utils,
  				logsService,
  				NgTableParams,
  				$state,
  				$window,
  				$scope,
  				$rootElement,
  				$element,
  				$compile,
  				$rootScope,
  				$q,
  				$interval){
  	    var instance=this;
  
  	    var log_operation = {
  			1:'扫描客户端',
  			2:'添加客户端(手动添加客户端)',
  			3:'删除客户端',
  			...
  		}
  
  	    instance.oprationColumns = [
  			{
  				field : "time",
  				title : "时间"
  			},
  			{
  				field : "operation",
  				title : "操作",
  				formatter : function (value, row, index) {
  					return log_operation[value];
  				}
  			},
  			{
  				field : "target",
  				title : "目标",
  				formatter : function (value, row, index) {
  					return value != 'NULL' ? value : '';
  				}
  			},
  			{
  				field : "msg",
  				title : "详细信息"
  			},
  			{
  				field : "result",
  				title : "结果",
  				formatter : function(value, row, index) {
  					return value=='no_need'?'非必须':(value=='success'?'成功':(value=='error'?'错误':'警告'))
  				}
  			}
  		];
  	    
  	    instance.runningColumns = [
  			{
  				field : "time",
  				title : "时间"
  			},
  			{
  				field : "msg",
  				title : "事件"
  			}
  		];
  	    
  	    instance.logs = [];
  	    instance.size = 0;
  	    
  	    // 刷新按钮
  	    instance.refresh = function() {
  	    	var params = {
      			'log_type':instance.log_type,
      			'offset':instance.logBean.offset,
      			'direct':instance.logBean.direct,
      			'fetch_count':instance.logBean.fetchCount
  	    	};
  	    	logsService.getLog(params).$promise.then(function(data) {
  	    		if(!(utils.statusHandler(data))){
  		    		return;		
  				}
  	    		instance.showLog(data);
  		    });
  	    };
  	    
  	    instance.$onInit = function(){
  			if ($rootScope.perm) {
  				instance.perm = JSON.parse($rootScope.perm);
  			}
  	    	instance.tableHeight = $($window).height()-$element.find('.title').outerHeight(true)-$element.find('.nav-tabs').outerHeight(true)-$element.find('.btn-tools').outerHeight(true)-70;
  	    	
  	    	instance.stateParams = $state.params;
  		    if(instance.stateParams['type']==0){
  		    	instance.columns=instance.oprationColumns;
  		    	instance.log_type = 0;
  		    }else if(instance.stateParams['type']==2){
  		    	instance.columns=instance.runningColumns;
  		    	instance.log_type = 2;
  		    }
  
  		    instance.goPageIndex = 1;
  		    instance.option = {
  	    		height : instance.tableHeight,
  	    		compile:function(){
  					utils.compile($scope,$element.find('table[bootstrap-table]'),$compile);
  				},
  	    		pageSize:20,
  	    		pageList:"[20,50]",
  	    		pagination : true,
  	    		columns : instance.columns,
  	    		queryParamsType:'',
  	    		queryParams:queryParams,
  	    		sidePagination: "server",
  	    		method:'post',
  	    		ajax:getLog,
  	    		singleSelect: false,
  				data : instance.logs
  		    };
  //	    	// getLogSelect
  //		    var params = {
  //				'log_type':instance.log_type,
  //				'fetch_count':instance.option.pageSize
  //			};
  //		    logsService.getLogSelect(params).$promise.then(function(data) {
  //		    	if(!(utils.statusHandler(data))){
  //		    		return;		
  //				}
  //		    	var logs = new Object();
  //		    	logs.total = data.data.total_count;
  //		    	var list = [];
  //		    	for (var i = 0; i < data.data.log.length; i++) {
  //		    		var log = new Object();
  //		    		log.time = data.data.log[i].time;
  //		    		log.operation = data.data.log[i].operation;
  //		    		log.result = data.data.log[i].result;
  //		    		log.prog_name = data.data.log[i].prog_name;
  //		    		log.msg = data.data.log[i].msg;
  //		    		list.push(log);
  //		    	}
  //		    	logs.rows = list;
  //		    	instance.logs = logs;
  //	    		$element.find('[bootstrap-table]').bootstrapTable('load',instance.logs);
  //		    });
  		    
  		    function getLog(params) {
  		    	if (instance.logBean.offset == 0) {
  		    		var param = {
  	    				'log_type':instance.log_type,
  	    				'fetch_count':instance.logBean.fetchCount
  		    		};
  		    		logsService.getLogSelect(param).$promise.then(function(data){
  			    		if(!(utils.statusHandler(data))){
  				    		return;		
  						}
  			    		instance.showLog(data);
  			    	});
  		    	} else {
  		    		var param = {
  	    				'log_type':instance.log_type,
  	    				'offset':instance.logBean.offset,
  	    				'direct':instance.logBean.direct,
  	    				'fetch_count':instance.logBean.fetchCount
  		    		};
  		    		logsService.getLog(param).$promise.then(function(data){
  		    			if(!(utils.statusHandler(data))){
  				    		return;		
  						}
  		    			instance.showLog(data);
  		    		});
  		    	}
  		    }
  	    };
  	    
  	    function queryParams(params){
  	    	instance.logBean = {
  	    		logType:instance.log_type,
  	    		fetchCount:params.pageSize,
  	    		offset:(params.pageNumber - 1) * params.pageSize,
  	    		direct:0
  	    	};
  	    	return instance.logBean;
  	    };
  	    
  	    instance.showLog = function (data) {
  	    	var logs = new Object();
  	    	logs.total = data.data.total_count;
  	    	var list = [];
  	    	for (var i = 0; i < data.data.log.length; i++) {
  	    		var log = new Object();
  	    		log.time = data.data.log[i].time;
  	    		log.operation = data.data.log[i].operation;
  				log.target = data.data.log[i].target;
  	    		log.result = data.data.log[i].result;
  	    		log.prog_name = data.data.log[i].prog_name;
  	    		log.msg = data.data.log[i].msg;
  	    		list.push(log);
  	    	}
  	    	logs.rows = list;
  	    	instance.logs = logs;
      		$element.find('[bootstrap-table]').bootstrapTable('load',instance.logs);
      		$element.find('[bootstrap-table]').bootstrapTable('hideLoading');
  			var pages=$element.find('[bootstrap-table]').bootstrapTable("getOptions").totalPages;
  			$('.page-list').append(('<span style="margin-left: 20px">前往</span><input style="margin: 0 10px" class="control-label" id="page" ng-model="$ctrl.goPageIndex" style="width: 60px"' +
  				' type="number"' +
  				' min="1"' +
  				' max="'+pages+'" ng-keydown="$ctrl.goPage(e)"><span>页</span>'));
  			utils.compile($scope,$('.page-list'),$compile);
  	    };
  
  		instance.goPage =  function(e) {
  			var theEvent = window.event || e;
  			var code = theEvent.keyCode || theEvent.which || theEvent.charCode;
  			if (code == 13) {
  				$element.find('[bootstrap-table]').bootstrapTable('selectPage', instance.goPageIndex)
  			}
  		};
  
  		instance.startInterval = function(){
  			if ($rootScope.getCompressLogStatusInterval) {
  				$interval.cancel($rootScope.getCompressLogStatusInterval);
  				$rootScope.getCompressLogStatusInterval = null;
  			}
  		};
  
  	/*	instance.stopInterval = function(){
  			return $q(function(resolve, reject){
  				if (!$rootScope.getCompressLogStatusInterval) {
  					$rootScope.getCompressLogStatusInterval = $interval(instance.getCompressLogStatus,3000);
  				}
  				resolve();
  			});
  		};*/
  	}]
  });
  ```

  该js文件首先会定义名为logsIndex的组件，templateUrl会加载该js文件对应的模板，即HTML，然后controller定义我们需要向视图（view）中添加的额外的功能，比如我们该模块中查询日志的操作就定义在其中，我们在controller中一般会定义一个初始化方法，即我们在加载模块的时候需要的操作，一般是获取页面初始化数据，所有初始化方法格式都是固定的，即instance.$onInit，instance是当前js文件的实例变量，$onInit方法名，后面的function函数为我们需要进行的操作，此初始化函数中会执行queryParams函数，instance.option中定义请求后台的所有属性，包括ajax属性即我们发送的请求，method请求类型等，此时发送的请求为logsService.getLog，而logsService为我们之前在service文件中定义的请求集，该请求实质上对应的后端控制器请求为/log/logGet，此时后端会收到前台发送过来的请求，后端的处理逻辑如下：

  

  - 后端

  ```java
  // ST_OP_LOG_GET
  @ApiOperation(value = "（从筛选结果中）获取日志", response = ApiResponse.class, notes =
                "1.Offset 表示从开始的偏移量\n" +
                "2.Direct 表示偏移的方向\n" +
                "   0 表示从最新记录开始偏移\n" +
                "   1 表示从最旧记录开始偏移")
  @PostMapping(value = "/logGet", produces = "application/json; charset=utf-8")
  public ApiResponse logGet (@RequestBody LogGetRequest resource) throws IOException{
      ApiResponse result = baseTransferService.transfer(resource, St_op_code.ST_OP_LOG_GET);
      if (result.getData() != null) {
          LogGetResponse logGetResponse = LogGetResponse.parseFrom((byte[]) result.getData());
          result = CommonDefine.protoToJson(result, logGetResponse);
      }
      return result;
  }
  ```

  该控制器中注入了BaseTransferService接口，该接口中定义了我们所有的操作业务方法，该接口的结构如下：

  ```java
  @Service(value = "baseTransferService")
  public interface BaseTransferService {
      // 常规操作
      <C extends ApiResponse,V extends GeneratedMessage> ApiResponse transfer(V request, long cmd) throws IOException;
  }
  
  ```

  我们在执行业务方法的时候主要是service接口的实现层，这里即BaseTransferServiceImpl，它的结构如下：

  ```java
  @Service
  public class BaseTransferServiceImpl implements BaseTransferService {
  
      @Autowired
      HttpSession session;
  
      @Autowired
      ApplicationPropertiesBean propertiesBean;
  
      /**
       * 常规操作
       * @param request
       * @param <C>
       * @param <V>
       * @return
       */
      @Override
      public   <C extends  ApiResponse, V extends GeneratedMessage>  ApiResponse  transfer(V request, long cmd) throws IOException {
          // 获取socket
          Socket socket = (Socket)session.getAttribute("socket");
          ApiResponse apiResponse = null;
          if (socket != null) {  // socket连接保持
              Header header = null;
              boolean sendFlag = false;
              header = SocketUtil.setHeader(cmd, request == null ? 0 : request.toByteArray().length);
              synchronized (socket){
                   sendFlag = SocketUtil.sendMessage(socket, header, request == null ? null : request.toByteArray());
                   if (sendFlag) {  // 消息发送成功
                       Map receive = null;
                       if (cmd == St_op_code.ST_OP_SCAN_CLIENTS) {  // 执行扫描客户端操作
                           receive = SocketUtil.scanClientsRecive(socket, header);
                       } else { // 其他操作
                           receive = SocketUtil.recive(socket, header);// 接收服务器响应数据
                       }
                       if ((boolean)receive.get("receiveFlag")) {  // 接收数据成功
                           Header headerResponse = (Header) receive.get("header");
                           byte[] protoByteResponse = null;
                           List list = new ArrayList();
                           if (cmd == St_op_code.ST_OP_SCAN_CLIENTS) {
                               list = receive.get("protoByte") != null ? (List)receive.get("protoByte") : null;
                           } else {
                               protoByteResponse = receive.get("protoByte") != null ? (byte[])receive.get("protoByte") : null;
                           }
                           if (headerResponse.getCmd() != 5 && headerResponse.getCmd() != 3 && headerResponse.getCmd() != 148 && headerResponse.getRetstatus() != 0) {
                               apiResponse = ApiResponse.successReturn(headerResponse.getRetstatus());
                           } else {
                               apiResponse = ApiResponse.successReturn(cmd == St_op_code.ST_OP_SCAN_CLIENTS ? list : protoByteResponse,
                                       headerResponse.getRetstatus());
                           }
                       } else {  // 接收数据失败
                           apiResponse = ApiResponse.failReturn(ApiCodeEnum.SYSTEM_ERROR);
                       }
                   } else {  // 发送失败
                       apiResponse = ApiResponse.failReturn(ApiCodeEnum.SYSTEM_ERROR);
                   }
               }
          } else {
              apiResponse = ApiResponse.failReturn(ApiCodeEnum.SYSTEM_ERROR);
          }
          return apiResponse;
      }
  }
  ```

  该实现层主要的逻辑是通过当前的session获取到对应的socket连接，通过该socket连接向服务端发送请求，请求由请求头和请求体组成，请求头格式固定，请求体为不同协议对应的request：

  请求体格式如下：

  ```java
  public class Header {
      public byte version;	//版本
      public byte msgtype;    
      public int retstatus;   //响应状态码
      public int flags;		
      public int from;
      public long cmd;  		// 操作码
      public long datalength=0L;  // 发送文件大小,单位为字节长度
  }
  ```

  服务端根据不同的操作码区分操作，操作码的定义在St_op_code类中，日志模块初始化方法的请求体为LogGetRequest，它是protobuf协议生成的Java类，实现层中会调用sendMessage发起请求到服务器，即

  ```java
  SocketUtil.sendMessage(socket, header, request == null ? null : request.toByteArray());
  ```

  该方法为静态方法，具体实现为:

  ```java
  /**
   * 发送消息到服务器
   * @param socket socket对象
   * @param header 消息头
   * @param bytes 发送消息体的byte数组
   */
  public static boolean sendMessage (Socket socket, Header header, byte[] bytes) throws IOException {
      boolean sendFlag = true;  // 发送消息是否成功
      // 获取输出流，向服务端发送数据
      OutputStream os = socket.getOutputStream();
      byte[] versionAndRetstatus = new byte[2];
      versionAndRetstatus[0] = header.getVersion();
      versionAndRetstatus[1] = header.getMsgtype();
      // 发送数据到服务端
      os.write(CommonDefine.byteMergerAll(versionAndRetstatus, CommonDefine.intToBytes(header.getRetstatus()),
                                          CommonDefine.intToBytes(header.getFlags()), CommonDefine.intToBytes(header.getFrom()),
                                          CommonDefine.longToBytes(header.getCmd()), CommonDefine.longToBytes(header.getDatalength())));
      if (bytes != null) {
          os.write(bytes);
      }
      os.flush();
      return sendFlag;
  }
  ```

  该方法接收一个socket实例，请求头对象，以及一个字节数组，通过socket实例获取到输出流将字节数组写入到流中flush到服务端完成向服务端的请求发送。

  服务端接收到请求后会处理响应，响应完成后会通过刚才的socket连接返回数据，主要通过方法SocketUtil.recive(socket, header)，也是一个静态方法，具体实现为：

  ```java
  /**
   * 接收服务器发送过来的数据
   * @param socket socket对象
   * @param header 消息头
   * @return
   */
  public static Map recive(Socket socket, Header header) throws IOException {
      boolean receiveFlag = true;
      Map map = new HashMap();
      // 获取输入流，读取来自服务器的数据
      InputStream is = socket.getInputStream();
      byte[] bytes = new byte[16];
      is.read(bytes);
      header.setVersion(bytes[0]);
      header.setMsgtype(bytes[1]);
      header.setRetstatus(CommonDefine.bytesToInt(bytes, 2));
      header.setFlags(CommonDefine.bytesToInt(bytes,4));
      header.setFrom(CommonDefine.bytesToInt(bytes,6));
      header.setCmd(CommonDefine.bytesToLong(bytes,8));
      header.setDatalength(CommonDefine.bytesToLong(bytes,12));  // 响应头设置完毕
      if (header.getCmd() == 0) {  // 服务器挂了
          throw new SocketException("服务器挂了");
      }
      if (header.getRetstatus() == 0) {  // 处理无误进行proto读取
          if (header.getDatalength() != 0) {
              // 需要返回数据
              long length = header.getDatalength();
              byte[] byteProto = new byte[(int)length];
              BufferedInputStream bfin = new BufferedInputStream(is);
              int step = 0;
              //int getNum=0;
              while (bfin.available()<length){
                  try {
                      Thread.sleep(100);
                  } catch (InterruptedException e) {
                      e.printStackTrace();
                  }
                  if (step++ >10000){
                      throw  new IOException("Read Socket Timeout");
                  }
              }
  
              int reedmun = bfin.read(byteProto,0,(int)length);
              map.put("protoByte", byteProto);
          }
      } else {
          map.put("protoByte", null);
  
          byte[] channels = new byte[(int)header.getDatalength()];
          is.read(channels);
          map.put("protoByte", channels);
      }
      // 返回header和服务器响应数据
      map.put("header", header);
      map.put("receiveFlag", receiveFlag);
      return map;
  }
  ```

  同发送请求类似。也是通过socket实例获取到输入流，然后将输入流中的数据读取到请求头中，如返回数据则将返回的数据方法接收的字节数组中，再通过不同的请求转换为不同的response，比如该例中就是转换为LogGetResponse，然后将数据封装到ApiResponse的data属性中，ApiResponse是前端与后端定义的数据交换格式，它的结构如下：

  ```java
  package cn.infocore.common;
  
  import java.io.Serializable;
  import java.util.Objects;
  
  import com.fasterxml.jackson.annotation.JsonProperty;
  
  import org.springframework.validation.annotation.Validated;
  
  import cn.infocore.exceptions.BusinessException;
  
  
  @Validated
  public class ApiResponse<T> implements Serializable {
  	@JsonProperty("code")
  	private Integer code = null;
  
  	@JsonProperty("data")
  	private T data = null;
  
  	@JsonProperty("message")
  	private String message = null;
  
  	@JsonProperty("status")
  	private Integer status = null;
  
  	public T getData() {
  		return data;
  	}
  
  	public void setData(T data) {
  		this.data = data;
  	}
  
  	public Integer getStatus() {
  		return status;
  	}
  
  	public void setStatus(Integer status) {
  		this.status = status;
  	}
  
  	public ApiResponse<T> code(Integer code) {
  		this.code = code;
  		return this;
  	}
  
  	/**
  	 * Get code
  	 * 
  	 * @return code
  	 **/
  
  	public Integer getCode() {
  		return code;
  	}
  
  	public void setCode(Integer code) {
  		this.code = code;
  	}
  
  	public ApiResponse<T> message(String message) {
  		this.message = message;
  		return this;
  	}
  	@SuppressWarnings({ "rawtypes", "unchecked" })
  	public static ApiResponse successReturn(Integer code) {
  		ApiResponse httpResponse = new ApiResponse();
  		ApiCodeEnum apiCodeEnum = ApiCodeEnum.SUCCESS;
  		httpResponse.setStatus(apiCodeEnum.getStatus());
  		httpResponse.setMsg(apiCodeEnum.getMsg());
  		httpResponse.setData(null);
  		httpResponse.setCode(code);
  		return httpResponse;
  	}
  
  	private void setMsg(String msg) {
  		this.message = msg;
  
  	}
  
  	public static <T> ApiResponse<T> successReturn(T data, Integer code) {
  		ApiResponse<T> httpResponse = new ApiResponse<T>();
  		ApiCodeEnum apiCodeEnum = ApiCodeEnum.SUCCESS;
  		httpResponse.setStatus(apiCodeEnum.getStatus());
  		httpResponse.setMsg(apiCodeEnum.getMsg());
  		httpResponse.setData(data);
  		httpResponse.setCode(code);
  		return httpResponse;
  	}
  
  	@SuppressWarnings({ "rawtypes", "unchecked" })
  	public static ApiResponse failReturn() {
  		ApiResponse httpResponse = new ApiResponse();
  		ApiCodeEnum apiCodeEnum = ApiCodeEnum.FAIL;
  		httpResponse.setStatus(apiCodeEnum.getStatus());
  		httpResponse.setMsg(apiCodeEnum.getMsg());
  		httpResponse.setData(null);
  		return httpResponse;
  	}
  
  	@SuppressWarnings({ "rawtypes", "unchecked" })
  
  	public static <T>  ApiResponse<T> failReturn(ApiCodeEnum apiCodeEnum) {
  		ApiResponse httpResponse = new ApiResponse();
  		httpResponse.setStatus(apiCodeEnum.getStatus());
  		httpResponse.setMsg(apiCodeEnum.getMsg());
  		httpResponse.setData(null);
  		return httpResponse;
  	}
  
  	@SuppressWarnings("rawtypes")
  
  	public static <T> ApiResponse failReturn(ApiCodeEnum apiCodeEnum, String message) {
  		ApiResponse<T> httpResponse = new ApiResponse<T>();
  		httpResponse.setStatus(apiCodeEnum.getStatus());
  		httpResponse.setMsg(message);
  		return httpResponse;
  	}
      @SuppressWarnings("unchecked")
      public static <T> ApiResponse failReturn(BusinessException businessException) {
          ApiResponse httpResponse = new ApiResponse();
          httpResponse.setStatus(businessException.getStatus());
          httpResponse.setMsg(businessException.getMessage());
          httpResponse.setData(null);
          return httpResponse;
      }
  
  	/**
  	 * Get message
  	 * 
  	 * @return message
  	 **/
  
  	public String getMessage() {
  		return message;
  	}
  
  	public void setMessage(String message) {
  		this.message = message;
  	}
  
  	@Override
  	@SuppressWarnings("rawtypes")
  	public boolean equals(java.lang.Object o) {
  		if (this == o) {
  			return true;
  		}
  		if (o == null || getClass() != o.getClass()) {
  			return false;
  		}
  		ApiResponse _apiResponse = (ApiResponse) o;
  		return Objects.equals(this.code, _apiResponse.code) && Objects.equals(this.data, _apiResponse.data)
  				&& Objects.equals(this.message, _apiResponse.message) && Objects.equals(this.status,
  				_apiResponse.status);
  	}
  
  	@Override
  	public int hashCode() {
  		return Objects.hash(code, data, message, status);
  	}
  
  	@Override
  	public String toString() {
  		StringBuilder sb = new StringBuilder();
  		sb.append("class ApiResponse {\n");
  
  		sb.append("    code: ").append(toIndentedString(code)).append("\n");
  		sb.append("    type: ").append(toIndentedString(data)).append("\n");
  		sb.append("    message: ").append(toIndentedString(message)).append("\n");
  		sb.append("    status: ").append(toIndentedString(status)).append("\n");
  		sb.append("}");
  		return sb.toString();
  	}
  
  	/**
  	 * Convert the given object to string with each line indented by 4 spaces
  	 * (except the first line).
  	 */
  	private String toIndentedString(java.lang.Object o) {
  		if (o == null) {
  			return "null";
  		}
  		return o.toString().replace("\n", "\n    ");
  	}
  }
  ```

  包含四个属性，分别为code，即服务端返回的状态码，该状态除了0为成功和2为已完成外其他所有状态都为失败，需要alert对应状态码的错误消息；data即服务端返回的响应数据，我们需要渲染的数据就放在其中；message即后端返回状态的消息，一般不显示，只给开发者作参考提示；status即后端处理的状态，前端根据该属性定义进行数据的显示或者异常的处理等等操作，该状态包括有以下几种：

  ```java
  /**
   * 成功返回
   */
  SUCCESS(200, "success"),
  /**
   * 失败返回
       */
  FAIL(400, "fail"),
  /**
       * 未认证
       */
  UNAUTHORIZED(401, "unauthorized"),
  /**
       * 拒绝访问
       */
  NOT_ALLOWED(403, "not allowed"),
  /**
       * 未找到资源
       */
  NOT_FOUND(404, "not found"),
  /**
       * 系统错误
       */
  SYSTEM_ERROR(500, "system error"),
  /**
       * 未授权
       */
  NOT_LICENSE(999, "not license");
  ```
  
  
  
  只有在状态为200时才成功，最后成功渲染数据如下，如图：
  
  ![](D:\Program Files (x86)\WXWork\zhangwei\sortware\photo\1580909943(1).jpg)

## 四、各模块具体实现功能

**<u>说明：括号中为操作对应的操作码</u>**

### 1、 登录模块

#### 1.1、登录

分别为普通登录与强制登录：

1. 普通登录（*ST_OP_LOGIN*）：当前登录用户未登陆时，此时可正常登录；

2. 强制登录（*ST_OP_LOGIN_FORCE*）：即当前登录用户已经登录在线，此时会提示用户是否强制登录，用户是否已经登录由服务端判断，强制登录后之前登录用户会下线；

   注意，登录还包括保持登录，保持登录是指登录后不会存在长时间不操作下线的情况，保持登录状态也是有服务端判断，web端只对服务端返回状态做对应处理。

#### 1.2、注销

注销（*ST_OP_LOGOUT*）功能主要是将当前用户与服务端的socket通信断开，并且将后端存储当前用户的信息从Map中清除并且返回到登录页面，此时是用户主动发起的注销请求；

注销还存在其他两种情况，一种是当root超级管理员上线后其他所有在线用户需强制下线，当其他用户发送任何请求时服务端都会返回下线通知，此时只有root用户在线，还一种请求就是用户未保持登录导致长时间未操作而超时下线，此时服务端会给后端发送请求告状该用户已离线，当该用户再次发送请求时后端会自行判断处理使其返回登录页面。

#### 1.4、授权

每个用户登录完成之后都会先检测一遍当前用户是否授权，此时会去获取授权信息（*ST_OP_GET_LIC_INFO*），若未授权或者授权过期则其他所有的请求无法进行，后端会判断后拦截请求，只有导入授权文件（*ST_OP_LIC_IMPORT*）服务端验证通过之后才能进行正常操作，试用版的用户和正式版的用户都可以进行正常操作。

#### 1.5、关于

该功能是当前使用版本的信息显示。

### 2、存储资源模块

该模块又分为两个子模块，分别为磁盘与存储空间

#### 2.1、磁盘

其中包含的是对streamer服务器磁盘的管理；

初始化该模块的时候首先会去回去磁盘的信息（*ST_OP_GET_SERVER_INFO*），初始状态是空白状态，即无磁盘，此时首先需要用户今天磁盘添加管理；

当进行添加操作时，首先页面需要知道streamer服务器有哪些可添加的磁盘，我们在加载页面的时候就获取到了磁盘的信息，自己判断那些磁盘已被添加和未被添加，将未被添加的磁盘显示在可添加列表中，此时如图：

![](https://github.com/liuershi/Images/blob/master/1580917291(1).jpg?raw=true)

此时我们可以选择需要添加的磁盘，可能存在磁盘信息不完整的情况，服务端可能未扫描处理部分磁盘，此时需要点击扫描按钮从新获取数据（*ST_OP_SERVER_DISK_RESCAN*），将获取到的数据重新显示到页面，此时我们就可以选择需要的磁盘添加到存储池了（*ST_OP_ADD_DISKS_TO_POOL*），不过正常的是，初次登录的时候是未配置存储池的，此时会添加失败，我们需要去添加存储池才能正确添加磁盘。

当我们添加完存储空间之后就可以正确添加磁盘到存储空间了，添加完的磁盘状态如图：

![](https://github.com/liuershi/Images/blob/master/企业微信截图_15809719849249.png?raw=true)

此时对于状态为在线的磁盘可以进行移除操作（*ST_OP_REMOVE_DISKS_TO_POOL*），而状态为离线的磁盘则也可以移除离线磁盘（*ST_OP_REMOVE_MISSING_FROM_POOL*）。

#### 2.2、存储空间

存储空间初始状态也是空白的，需要添加（*ST_OP_SET_FILE_BACKUP_SPACE*），默认只能添加文件备份空间，如图所示：

![](https://github.com/liuershi/Images/blob/master/企业微信截图_15809708978763.png?raw=true)

添加完存储空间后，我们就可以对该存储空间做一些操作：

![](https://github.com/liuershi/Images/blob/master/企业微信截图_158097100122.png?raw=true)

比如说编辑（*ST_OP_UPDATE_FILE_BACKUP_SPACE_DISASTER_STRATEGY*），即改变我们创建存储空间时的容量策略；

移除（*ST_OP_DEL_FILE_BACKUP_SPACE*），将我们创建的存储空间从streamer上删除；

重载（*ST_OP_RELOAD_FILE_BACKUP_SPACE*），页面可以出现移除失败服务端配置错乱问题，通过重载从新获得最新数据；

### 3、客户端模块

#### 3.1、客户端增删

客户端模块是该项目中最重要也是最复杂的模块，初始化时无客户端，需要添加客户端，分为手动添加与自动添加两种：

- 手动添加（*ST_OP_ADD_CLIENTS*）

  根据IP添加对应的客户端

  ![](https://github.com/liuershi/Images/blob/master/企业微信截图_15809724273718.png?raw=true)

- 自动添加（*ST_OP_SCAN_CLIENTS*）

  根据streamer所处的网段扫描处于同网段的客户端选择添加

  ![](https://github.com/liuershi/Images/blob/master/企业微信截图_15809730893291.png?raw=true)

添加完成客户端后，也可以对客户端进行移除操作（*ST_OP_DEL_CLIENTS*）；

#### 3.2、数据库

客户端添加完成后，我们会得到对应客户端中的数据，包括磁盘信息，数据库信息等等，数据渲染完成效果如下：

![](https://github.com/liuershi/Images/blob/master/企业微信截图_15809733493170.png?raw=true)

在完成对客户端的添加删除操作后，我们可以对客户端中其他信息进行操作，比如说数据库操作：

- 配置数据库信息（*ST_OP_DB_SET*）
- 取消数据库的配（*ST_OP_DBCFG_DEL*）

#### 3.3、一致性组

- 创建一致性组（*ST_OP_BG_CREATE*）

  添加完客户端初始状态时是无一致性组的，首先可以创建一致性组，通过指定一致性组名创建，一致性组不存在类型为分区的情况，默认为磁盘：

  ![](https://github.com/liuershi/Images/blob/master/企业微信截图_15809741262641.png?raw=true)

- 删除一致性组（*ST_OP_DEL_BACKUP_GROUP*）

  一致性组也可以删除，若组中存在磁盘则组中磁盘不在属于任何组；

- 一致性组管理

  一致性组中若无磁盘我们则可以给该一致性组添加磁盘（*ST_OP_ADD_DISK_TO_BG*），需要保证的是，磁盘与组状态是一致的，即磁盘与组都无备份或者同时存在备份才能添加成功，否则都需要进行相应的备份处理；还可以从组中移除磁盘（*ST_OP_REM_DISK_FROM_BG*）

#### 3.4、磁盘

之前在操作一致性组的时候，我们可以选定磁盘添加到一致性组，同时也可以直接操作磁盘添加到一致性组中，操作与前者也是一样的；

- 添加备份（*ST_OP_ADD_BACKUP*）

  对于初始状态的磁盘，我们首先需要添加备份，添加备份向导如图：

  ![](https://github.com/liuershi/Images/blob/master/企业微信截图_15809752259106.png?raw=true)

  首先需要测试服务端与客户端（*ST_OP_ESTABLISH_CHANNELS*），分为网络备份与光纤备份，他们的测试都是同一个操作码；

  在测试通过之后才能到下一步配置保存卷的部分：

  ![](https://github.com/liuershi/Images/blob/master/企业微信截图_15809755888682.png?raw=true)

  在这部分我们需要配置磁盘的一些配置信息，在配置信息输入合法的情况下可以到下一步设置任务计划部分：

  ![](https://github.com/liuershi/Images/blob/master/企业微信截图_15809757214034.png?raw=true)

  默认情况下配置快照策略是不勾选的，我们可以开启快照合并策略：

  ![](https://github.com/liuershi/Images/blob/master/企业微信截图_15809758487043.png?raw=true)

  默认情况下是无合并策略的，我们可以通过策略管理删除或者新增策略：

  - 新增策略（*ST_OP_CREATE_CDP_CONSOLID_POLICY*）

  - 删除策略（*ST_OP_DELETE_CDP_CONSOLID_POLICY*）

    ![](https://github.com/liuershi/Images/blob/master/企业微信截图_15809761111421.png?raw=true)

  配置完任务计划后，可以到下一步的同步设置，该部分是设置该备份的同步与异步设置：

  ![](https://github.com/liuershi/Images/blob/master/企业微信截图_15809762512245.png?raw=true)

  在完成同步设置后，在确认完配置无误后就可以给客户端添加备份了，向导中包含的所有操作都是为该操作做的一些设置。

- 删除备份（*ST_OP_DEL_BACKUP*）

  有备份的创建就必然有备份的删除，该操作是将磁盘或组的备份删除；

- 同步数据（*ST_OP_INIT_MIRROR*）

  当我们添加备份的时候未选择立即同步可以手动同步备份计划；

- 取消同步数据（*ST_OP_CANCEL_INIT_MIRROR*）

  数据同步是一个过程，在此过程中我们可以取消该备份的数据同步；

- 修改任务计划（*ST_OP_SET_CDP_SCHEDULE*）

  对于已经添加的备份，我们可以修改添加备份时设置的任务计划，修改任务计划时的参数和添加任务计划时一致；

  ![](https://github.com/liuershi/Images/blob/master/企业微信截图_1580977713653.png?raw=true)

- 修改同步设置（*ST_OP_SET_HOSTMIRROR*）

  同任务计划一样，都是在添加备份时设置的，可以单独修改；

  ![](https://github.com/liuershi/Images/blob/master/企业微信截图_1580977886471.png?raw=true)

- 配置保存卷（*ST_OP_UPDATE_RESIZE*）

  同样该操作也是添加备份时设置，也可以单独修改；

  ![](https://github.com/liuershi/Images/blob/master/企业微信截图_15809780021595.png?raw=true)

- 手动创建快照（*ST_OP_CREATE_SNAPSHOT*）

  对于已经添加备份的磁盘或组我们可以给其创建快照；

  ![](https://github.com/liuershi/Images/blob/master/企业微信截图_15809783343277.png?raw=true)

- 快速恢复

  当我们创建完快照之后就可以根据创建的快照进行恢复操作；

  ![](https://github.com/liuershi/Images/blob/master/企业微信截图_15809786387680.png?raw=true)

  默认选定的是最新的快照，然后选定需要恢复的模式，物理机或虚拟机，此时显示的Initiator IP很光纤通道中的Initiator WWN和Target WWN都是通过获取恢复快照通道（*ST_OP_GET_CHANNELS_FOR_RESTORE*）这个操作从服务端获取的。

  ![](https://github.com/liuershi/Images/blob/master/企业微信截图_15809787504711.png?raw=true)

  ![](https://github.com/liuershi/Images/blob/master/企业微信截图_15809795763590.png?raw=true)

  然后选择需要恢复的虚拟机通道，存在网络通道和光纤通道，最后将向导中选定的额参数提交发起恢复请求（*ST_OP_SNAP_RESTORE*）。

我们也可以通过查看详情获取磁盘或组的具信息，如下图：

![](https://github.com/liuershi/Images/blob/master/企业微信截图_15809790339222.png?raw=true)

该图中显示了磁盘的基本信息以及备份信息，基本信息即磁盘的硬件信息，备份信息为我们创建备份时添加的信息，还存在快照管理，此时显示的是该磁盘所有的快照信息（*ST_OP_GET_SNAPS_INFO_BY_BIRTH_DATE*），而图表中的数据则是从服务端文件中读取显示的（*ST_OP_GET_REALSNAPS_INFO_BY_BIRTH_DATE*），其中的刷新和查看操作都是再获取一遍数据，而恢复操作同前面的快速恢复操作一致，快速挂载（*ST_OP_REMAP_DISK_TO_ORIGINAL_CLIENT*）操作作用也同恢复一致。

其中，快照列表中还存在对磁盘快照的其他操作，根据快照的恢复状态和使用状态不同操作也不一样：

- 未恢复，未使用

  ![](https://github.com/liuershi/Images/blob/master/企业微信截图_15809797154780.png?raw=true)

  其中包括了快速挂载，恢复，删除，保留快照四个操作，前两个操作和前面一样：

     	删除（*ST_OP_DEL_SNAPSHOT*）：即删除当前快照；

  ​	   保留快照（*ST_OP_SAVE_SNAPSHOT*）：即将当前快照状态锁定；

  ​	   取消保留快照（*ST_OP_CANCEL_SAVE_SNAPSHOT*）：当快照被保留后，状态会变为保留状态，可以通过取消保留操作使状态变为未锁定；

- 已恢复，已使用

  ![](https://github.com/liuershi/Images/blob/master/企业微信截图_1580980173136.png?raw=true)

  包括在线回迁，取消恢复，删除，保留快照等四个操作，其中在线回迁操作又包含全量拷贝和增量拷贝两种情况：

  ​		全量拷贝：

  ​			首先，需要测试恢复的目标IP地址（*ST_OP_RESTORE_TEST_IP*）

  ​			![](https://github.com/liuershi/Images/blob/master/企业微信截图_15809817869034.png?raw=true)

  ​			测试通过之后可以添加对应的本地磁盘与目标磁盘，此时数据需要向服务器获取（*ST_OP_GET_SERVER_CLIENT_DISK_LIST*）

  ​			![](https://github.com/liuershi/Images/blob/master/企业微信截图_15809818709780.png?raw=true)

  ​			选择需要添加到额本地磁盘与目标磁盘后进行全量恢复操作（*ST_OP_TWICE_RESTORE_FIRST*）。

  ​		增量恢复：

  ​			当进行全量恢复完后可进行增量恢复（*ST_OP_TWICE_RESTORE_SECOND*）。

  ​		取消全量恢复：

  ​			可以取消二次恢复中第一次，第二次恢复，取消恢复后状态为已恢复，已使用的状态（*ST_OP_CANCEL_TWICE_RESTORE*）。	

  ​		终止恢复：

  ​			该命令用于当第一次,第二次恢复失败时使用，用于终止恢复，恢复到上一个状态（*ST_OP_STOP_TWICE_RESTORE*）。

  ​		取消恢复：

  ​			因为此时快照的状态为已恢复，所以可以进行取消恢复（*ST_OP_CANCEL_RESTORE*）操作使快照状态变为未恢复。

- 已恢复，未使用

  ![](https://github.com/liuershi/Images/blob/master/企业微信截图_15809835174963.png?raw=true)

  与之前的状态相比，多了一个再次恢复操作，该操作与快速恢复一致。

#### 3.5、应急接管

该功能的作用是用于创建kvm虚拟机，创建kvm虚拟机首先需要保证kvm宿主机的额存在，若未配置kvm宿主机则需要先在系统设置模块中的应急接管中添加宿主机，添加完宿主机之后，还需要保证当前客户端的系统盘处于被保护的状态，当这两个条件都满足时才能开始应急接管的向导：

![](https://github.com/liuershi/Images/blob/master/企业微信截图_1581167929471.png?raw=true)

在开始向导时首先需要获取当前客户端中已保护磁盘或组的所有快照（*ST_OP_GET_SNAPS_INFO_BY_BIRTH_DATE*），在向导中默认会选中系统盘且不能取消，我们也可以选择其它已保护的磁盘，但是必须保证所有选择的磁盘有快照且快照的状态为未恢复，否则无法进行下一步操作，当这些条件都满足时就可以进行下一步了：

![](https://github.com/liuershi/Images/blob/master/企业微信截图_15811682371595.png?raw=true)

由界面可知，到达此页面时我们需要显示当前kvm宿主机的可用硬件信息，此时就需要获取可用的kvm硬件信息（*ST_OP_KVM_GET_AVAILABLE_HARDWARE_INFO*），比如说CPU数量，内存大小，主机网卡等等信息，最后输入合法的参数配置下就可以添加kvm虚拟机了（*ST_OP_KVM_CREATE*），创建成功的kvm虚拟机可以在应急接管模块中看的。

**注意：磁盘的所有操作组也是一样可以执行的！**

### 4、文件备份模块

文件备份模块中共包含三个子模块，分别为客户端模块，备份计划模块，恢复任务模块。

#### 4.1、客户端

该模块是管理文件备份客户端的模块，主要功能包括客户端的添加，备份计划的创建，备份计划的恢复以及文件备份客户端的删除等。

##### 4.1.1、客户端添加

通过客户端IP添加指定的客户端（*ST_OP_FILE_BACKUP_ADD_CLIENT*）

![](https://github.com/liuershi/Images/blob/master/企业微信截图_15809951189106.png?raw=true)

##### 4.1.2、删除客户端

添加完成的文件备份客户端可以选择删除（*ST_OP_FILE_BACKUP_DEL_CLIENT*）

##### 4.1.3、创建备份

我们可以选定一个客户端为其创建备份计划（*ST_OP_FILE_BACKUP_ADD_BACKUP*）

首先需要指定备份计划的名称，名称不可重复：

![](https://github.com/liuershi/Images/blob/master/企业微信截图_15810091432670.png?raw=true)

设置完名称之后需要选择保护对象：

![](https://github.com/liuershi/Images/blob/master/企业微信截图_15810092931458.png?raw=true)

在这个过程中，我们需要指定所包含或者排除的对象，此时我们需要获取服务器的文件目录（*ST_OP_FILE_BACKUP_GET_CLIENT_FILE_LIST*），而且还需要获取指定文件夹下的其他文件或文件夹（*ST_OP_FILE_BACKUP_GET_CLIENT_FILE_LIST*）。

制定完保护对象之后，就需要指定备份计划保存的位置，通常是存储资源的文件备份空间：

![](https://github.com/liuershi/Images/blob/master/企业微信截图_15810096403598.png?raw=true)

若文件备份空间正常添加，即空间大小足够，在进行备份策略的设置，与普通客户端中添加备份设置策略类似：

![](https://github.com/liuershi/Images/blob/master/企业微信截图_15810098334845.png?raw=true)

最后设置完毕确认配置后就可以发送添加备份保护的请求（*ST_OP_FILE_BACKUP_ADD_BACKUP*），需要注意的是客户端离线状态下无法进行此操作。

##### 4.1.4、恢复

该功能的主要作用是根据一个备份计划的备份点将某个文件或文件夹恢复到原机或者下载到本机。

在客户端模块中恢复时首先需要选择客户端包含的备份计划，那么就需要获取到这些备份计划信息（*ST_OP_FILE_BACKUP_GET_CLIENTS*）：

![](https://github.com/liuershi/Images/blob/master/企业微信截图_15810105181029.png?raw=true)

需要注意，若备份计划状态为恢复中时则无法选择，选择完备份计划后需要选择对应的备份点：

![](https://github.com/liuershi/Images/blob/master/企业微信截图_15810106394724.png?raw=true)

这些备份点的创建是在备份计划模块完成的，我们在后面将这部分，然后选择一个时间点，然后需要选择恢复的文件：

![](https://github.com/liuershi/Images/blob/master/企业微信截图_15810108861602.png?raw=true)

在选择文件时，张开层级目录显示文件和文件夹的操作与添加备份选定保护对象规则操作一致。，选定文件后，我们可以选择是恢复到原机还是下载，默认为恢复到原机：

![](https://github.com/liuershi/Images/blob/master/企业微信截图_15810110503693.png?raw=true)

恢复至原机又分为覆盖恢复与自定义恢复，区别只在于是否自己指定恢复路径（*ST_OP_FILE_BACKUP_RESTORE_TO_OVERWRITE*）；另外下载操作会将恢复计划下载到本机，即操作机器上（*ST_OP_FILE_BACKUP_RESTORE_TO_OVERWRITE*），需要注意的是客户端离线状态下无法进行此操作。

#### 4.2、备份计划

备份计划为在客户端模块中指定某个客户端创建的，每个备份计划都有所属的客户端：

![](https://github.com/liuershi/Images/blob/master/企业微信截图_15810113719302.png?raw=true)

每个备份计划包括的操作有恢复，增量备份，全量备份，修改备份，删除，查看详情等等。



与客户端模块中恢复操作一样，只是不需要选择某个备份计划。

##### 4.2.2、全量备份与全量备份

给备份计划添加备份点（*ST_OP_FILE_BACKUP_RESTORE_TO_LOCAL*），若当前备份计划正在备份时无法操作。

##### 4.2.3、修改备份

作用是修改该备份计划在创建时设置（*ST_OP_FILE_BACKUP_MODIFY_BACKUP_PLAN*）：

![](https://github.com/liuershi/Images/blob/master/企业微信截图_15810119263566.png?raw=true)

##### 4.2.4.删除

删除我们选择的备份计划（*ST_OP_FILE_BACKUP_DELETE_RESTORE_PLAN*），正在恢复的备份计划无法删除。

##### 4.2.5、查看详情

会获取关于此任务的信息，包括任务名称，保护对象，保存位置，备份策略以及备份点信息等等：

![](https://github.com/liuershi/Images/blob/master/企业微信截图_15810128398611.png?raw=true)

其中包含了对快照电动额恢复以及删除操作恢复操作与对备份计划的恢复操作一致，只是不需要选择会的备份点，而删除操作会删除指定的备份点（*ST_OP_FILE_BACKUP_DELETE_BACKUP_BRANCH*），默认只能删除最老得快备份点。

#### 4.3、恢复任务

恢复任务有备份计划恢复至原机时创建的，加载恢复任务需要的数据（*ST_OP_FILE_BACKUP_GET_RESTORE_PLAN*），包含操作有取消，删除等。

##### 4.3.1、取消

作用是将正在恢复的任务直接取消（*ST_OP_FILE_BACKUP_CANCEL_RESTORE_PLAN*），只有处于恢复中状态的恢复任务才能进行此操作。

##### 4.3.2、删除

将已完成或失败的任务计划删除（*ST_OP_FILE_BACKUP_DELETE_RESTORE_PLAN*），正在恢复中的任务计划无法进行此操作。

### 5、应急接管模块

该模块中的数据是在客户端模块应急接管中配置的，获取该模块数据操作为（*ST_OP_KVM_GET_ALL_VMS_INFO*），获取数据如下：

![](https://github.com/liuershi/Images/blob/master/企业微信截图_15810133325023.png?raw=true)

主要包括的操作有开启kvm，关闭kvm，全量拷贝，增量恢复，获取快照信息，连接vnc，删除kvm虚拟机等等。

##### 5.1、关闭kvm

从客户端模块应急接管到该模块时创建的kvm虚拟机默认状态为开机，此时我们可以关闭kvm虚拟机（*ST_OP_KVM_FORCE_SHUTDOWN*）。

##### 5.2、开启kvm

当kvm虚拟机状态为关机时，我们就可以开启kvm虚拟机了（*ST_OP_KVM_BOOT*）。

##### 5.3、全量拷贝

根据在线回迁流程图我们可知，初始创建的kvm虚拟机状态为已恢复已使用，此时我们可以进行全量拷贝，在全量拷贝的时候我们需要先测试恢复目标的IP（*ST_OP_RESTORE_TEST_IP*）：

![](https://github.com/liuershi/Images/blob/master/企业微信截图_15810139633016.png?raw=true)

测试完IP后继续下一步添加本地磁盘与目标磁盘，该过程与客户端中快照点二次回迁操作一致：

![](https://github.com/liuershi/Images/blob/master/企业微信截图_15810141378739.png?raw=true)

选择 需要添加的磁盘后直接进行恢复操作（*ST_OP_TWICE_RESTORE_FIRST*）。

##### 5.4、增量恢复

同客户端模块中操作一致。

##### 5.5、查看快照

主要是查看当前kvm虚拟机所包含的快照（该操作需要显示的快照信息包含在获取kvm虚拟机信息中）。

![](https://github.com/liuershi/Images/blob/master/企业微信截图_15810144591609.png?raw=true)

##### 5.6、删除

删除kvm虚拟机，需要注意的是，处于开机状态无法进行此操作（*ST_OP_KVM_DELETE*）。

##### 5.7、连接vnc

通过kvm服务端给定的端口和IP，将麒麟服务器桌面显示在web端（*ST_OP_CONNECT_VNC*）。

### 6、容灾配置模块

该模块又细分为容灾服务器和普通容灾客户端，其中又以容灾客户端为重。

#### 6.1、容灾服务器

容灾服务器的作用主要是在容灾客户端添加容灾关系时使用，除此之外，我们还可以对荣在服务器做一些其他的操作，比如说修改密码，修改流量上限，修改服务器IP移除移除已添加的服务器等等。

![](https://github.com/liuershi/Images/blob/master/企业微信截图_158113613922.png?raw=true)

##### 6.1.1、添加容灾服务器

初始状态时无容灾服务器，此时我们可以根据服务器名、服务器IP、用户名、用户密码等添加一台容灾服务器（*ST_OP_ADD_DR_SERVER*），如图所示：

![](https://github.com/liuershi/Images/blob/master/企业微信截图_15811359498763.png?raw=true)

其中，服务器名和IP需自己指定，用户名与密码初始时为root与infocore。

##### 6.1.2、修改密码

对于容灾服务器的密码也可以修改（*ST_OP_CHANGE_DR_PASSWORD*），只需要指定新密码即可。

![](https://github.com/liuershi/Images/blob/master/企业微信截图_15811365869249.png?raw=true)

##### 6.1.3、修改流量上限

我们可以指定新的流量上限也可以直接指定为无上限（*ST_OP_SET_DR_MAX_BANDWIDTH*）。

![](https://github.com/liuershi/Images/blob/master/企业微信截图_15811367693718.png?raw=true)

##### 6.1.4、配置IP

我们可以给容灾服务器配置多个IP，可以添加可以删除。

- 添加IP（*ST_OP_ADD_DR_SERVER_IP*）

  只需要输入需要添加的IP即可。

  ![](https://github.com/liuershi/Images/blob/master/企业微信截图_15811369303291.png?raw=true)

- 删除IP（*ST_OP_DELETE_DR_SERVER_IP*）

  同理，只需要指定已添加需要删除的IP即可。

##### 6.1.5、移除容灾服务器

需要注意是，若当前容灾服务器存在容灾关系则无法删除，需要先移除存在的容灾关系（*ST_OP_DELETE_DR_SERVER*）。

#### 6.2、普通容灾客户端

添加容灾服务期之后，我们可以根据荣在服务器添加对应的容灾关系，然后对添加的容灾关系做一些列的操作。

##### 6.2.1、添加容灾关系

添加完容灾关系需要进行一系列的向导，首先我们需要选择添加容灾关系的客户端，该客户端是客户端模块中的客户端，其次需要指定该客户端中一个磁盘或一致性组，并且该磁盘或组的状态必须是已备份的：

![](https://github.com/liuershi/Images/blob/master/企业微信截图_15811377303170.png?raw=true)

设置完成后，我们需要指定之前添加的容灾服务器，而且离线状态的服务器无法被选择：

![](https://github.com/liuershi/Images/blob/master/企业微信截图_15811378762641.png?raw=true)

指定完服务期之后，需要配置保存卷，同客户端模块中添加备份同理：

![](https://github.com/liuershi/Images/blob/master/企业微信截图_15811379869106.png?raw=true)

指定完保存卷后设置任务计划，这里的设置同添加备份一模一样，只是他的属性是容灾的，不是普通客户端类型的：

![](https://github.com/liuershi/Images/blob/master/企业微信截图_15811380918682.png?raw=true)

最后需要设置传输配置，指定传输协议以及cdp快照，传输协议类型有TCP和UDP两种，而CDP快照则分为新建CDP快照点与原有CDP快照点，还可以是否开启数据加密和数据压缩等等配置：

![](https://github.com/liuershi/Images/blob/master/企业微信截图_15811381844034.png?raw=true)

最后，我们确认完配置之后就可以添加容灾关系了（*ST_OP_SET_DR_RELATIONSHIP*）。

添加完容灾关系后就可以进行其他操作了，添加完的容灾关系如下，当然我们首先要先获取已添加的容灾关系（*ST_OP_GET_DR_RELATIONSHIP*），获得的容灾关系如下：

![](https://github.com/liuershi/Images/blob/master/企业微信截图_15811383467043.png?raw=true)

##### 6.2.2、手动复制

该操作主要是对我们容灾关系中添加的磁盘或一致性组进行容灾复制，即复制磁盘或组中的数据，对于磁盘来说只需要传磁盘名而组只需要传一致性组名即可（*ST_OP_CREATE_DR_REPLICATION_MANNUAL*）。

##### 6.2.3、取消复制

该操作是相对于手动复制的，只有在容灾关系状态为复制中时才能进行此操作（*ST_OP_CANCEL_DR_CREATING_REPLICATION*）。

##### 6.2.4、查看复制记录

这个操作也是对于手动复制而言，作用是查询我们做过的手动复制的记录（*ST_OP_GET_DR_REPLICATION_BY_BIRTH_DATE*）。

##### 6.2.5、修改任务计划

该操作类似客户端模块添加备份中的修改任务计划，区别在于是否是容灾客户端而已（*ST_OP_SET_DR_REP_SCHEDULE*），这其中还包括对快照合并策略的管理操作，也是等同于客户端模块中的策略管理操作，区别在于是否是荣在属性。

##### 6.2.6、配置保存卷

该操作也是通修改任务计划一样，与客户端模块中的配置保存卷操作一样，只通过是否是容灾属性区分两者。

##### 6.2.7、修改传输设置

该操作修改在添加容灾关系时设置的传输设置，可修改的类型与添加时一致（*ST_OP_SET_DR_TRANSFER*）。

##### 6.2.7、移除容灾关系

移除添加的容灾关系（*ST_OP_DEL_DR_RELATIONSHIP*）。

### 7、系统日志模块

该模块主要是保存程序运行执行过程中的所有记录，分为操作日志和运行日志两类，前者是用户操作程序所执行的所有操作，而后者则是系统后台运行做的操作，该模块中的主要操作包括日志的获取，日志筛选，日志的压缩及下载等等。

- 日志获取

  进入系统日志模块默认显示为操作日志，此时需要显示所有的操作记录，那就需要获取日志信息（*ST_OP_LOG_SELECT*），不管是操作日志还是运行日志操作码都是一样的，只是通过一个type类型区别。

- 日志筛选

  日志是大量的，页面的显示是有限的，所以需要通过分页来处理显示所有的日志信息，当用户需要跳转到其他页查看日志信息时就需要该操作了（*ST_OP_LOG_GET*），该操作的实现是通过偏移方向和偏移量实现的。

- 日志压缩

  对于日志来说，我们有时候需要下载下来，这时候就需要用到日志压缩了，对于日志压缩来说，我们需要指定压缩那些客户端的日志，需要注意的是对于离线的客户端我们是无法选择的，只能压缩在线客户端的日志（*ST_OP_COMPRESS_LOG*）。

- 日志下载

  对于压缩好的日志我么就可以下载了，选择我们需要下载的日志，这个可以选择的日志是需要获取的，首先获取能下载的压缩日志列表（*ST_OP_GET_COMPRESSED_LOG_LIST*），获取到了之后选择需要下载的日志（*ST_OP_LOG_EXPORT*），注意，下载日志时只能单选。

### 8、系统设置模块

该模块中共包含四个子模块，分别为用户管理，服务器通道，网络配置，应急接管配置等。

#### 8.1、用户管理

该模块的作用是对用户的curl管理，需要注意的是，除了修改密码操作外其他操作只能是管理员操作，初始时管理员有超级管理员root和普通管理员admin，它们的初始密码分别为passw0rd与admin，同时当root在线时其他所有用户则必须离线。

##### 8.1.1、显示用户列表

当选择用户模块时，首先会加载已存在的用户信息，此时需要获取用户列表信息（*ST_OP_REGISTERED_USERS*）。

##### 8.1.2、创建用户

该操作只能有管理员，不能创建相同用户名的用户（*ST_OP_ADDUSER*），所有创建的用户权限都是普通用户。

##### 8.1.3、修改密码

所有修改密码操作都是能使当前登录用户修改自己的密码（*ST_OP_CHANGE_PASSWD*）。

##### 8.1.4、重置密码

该操作也是能是管理员操作，同时，当当前用户为root时，则可以重置所有用户的密码，若为admin用户时则可以重置所有普通用户的密码（*ST_OP_RESET_PASSWD*）。

##### 8.1.5、删除用户

该操作也只能是管理员用户删除普通用户（*ST_OP_DELUSER*）。

#### 8.2、服务器通道

作用是对于iscsi和FC通道的管理，功能包括对FC通道的切换，需要注意的是，此模块只对管理员显示。

加载该模块时，首先会去获取服务器通道信息（*ST_OP_GET_SERVER_CHANNELS*），包括ISCSI和FC的，默认显示ISCSI通道的信息，此时无其他操作，我们可以选择显示FC的通道信息，对于FC通道来说，我们可以选择切换通道的模式（*ST_OP_SET_FC_MODE*），存在两种模式，分别为Target和Initiator两种，处于那种模式选择切换就会跳转到另外一种模式。

#### 8.3、网络配置

该模块是对网卡以及bond的管理操作，我们可以管咯bond组中的网卡，包括删除和添加，也可以修改网卡和bond组的IP等等。

加载该模块需要先获取网络配置信息（ST_OP_GET_SERVER_NETWORKING），包括bond以及网卡的信息，初始状态时是无bond组的，需要我们先创建一个bond组。

##### 8.3.1、创建bond组

这个操作需要分为两步完成，首先我们需要指定添加到bond组的网卡，已添加到其他组的网卡不能被添加，可以添加多个网卡，同时指定成组的模式：

![](https://github.com/liuershi/Images/blob/master/企业微信截图_15811617751421.png?raw=true)

组的模式有适配器传输负载均衡器，轮询，IEEE 动态链接聚合等三种，选择完网卡和成组模式后就可以下一步了，设置网卡的配置信息，配置信息包括bond组的IP地址、子网掩码、默认网、首选DNS服务器、备用DNS服务器等：

![](https://github.com/liuershi/Images/blob/master/企业微信截图_15811619982245.png?raw=true)

设置完成后就可以创建bond组了（*ST_OP_BOND_CREATE*），创建完成后会重启网络配置并回到登录页。

##### 8.3.2、bond组管理

对于bond组来说，其中的管理操作包括对网卡的添加以及移除。

- 添加网卡（*ST_OP_ADD_DEVICE_TO_BOND*）

  添加完成后会重启网络配置并回到登录页。

- 移除网卡（*ST_OP_DEL_DEVICE_FROM_BOND*）

  移除网卡后也会重启网络配置并回到登录页。

##### 8.3.3、修改IP

修改bond组或网卡的IP信息（*ST_OP_SET_SERVER_NETWORKING_IP*），修改完IP后会重启网络配置并回到登录页。

![](https://github.com/liuershi/Images/blob/master/企业微信截图_1581164185653.png?raw=true)

##### 8.3.4、移除bond组

创建 bond组也可删除（*ST_OP_DEL_BOND*），删除后会重启网络配置并回到登录页。

#### 8.4、应急接管配置

该模块作用是对kvm宿主机的管理，包括宿主机的添加、移除更新IP等操作，当然加载该模块时首先会获取宿主机信息（*ST_OP_GET_KVM_SERVER*）。

##### 8.4.1、添加宿主机

该操作只能管理员权限用户操作，同时最多只能添加一台宿主机（*ST_OP_ADD_KVM_SERVER*）。

##### 8.4.2、移除宿主机

在执行该操作时，可能存在kvm虚拟机，若存在KVM虚拟机，不勾选强制删除，则提示有KVM不让删;

勾选强制删除,则有二次提示,然后删除宿主机和KVM虚机及配置（*ST_OP_DEL_KVM_SERVER*）。

##### 8.4.3、更新IP

更新宿主机IP，需要注意的是更新完成后宿主机需要重启网络配置这样会导致宿主机状态异常（*ST_OP_UPDATE_KVM_SERVER_IP*）。

## 五、打包及运行

本项目以maven插件方式打成可执行jar包，在将jar打成RPM包运行安装。

maven插件依赖：

```xml
<build>
    <plugins>
        <plugin>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.8.1</version>
            <configuration>
                <fork>true</fork>
                <executable>
                    C:\Program Files (x86)\Java\jdk1.8.0_231\bin\javac.exe
                </executable>
            </configuration>
        </plugin>
    </plugins>
</build>
```

jdk的路径需要修改为自己本机的jdk路径,指定xxx-client模块的启动类为主启动类。

以命令行的形式执行打包命令：

```java
mvn clean package
```

得到名为streamer-interface-web-service-client-0.0.1-SNAPSHOT.jar的可执行jar包，将其更名为stmweb.jar。

以192.168.1.201为打包平台，rpmbuild目录结构：

```shell
├── BUILD
├── BUILDROOT
├── RPMS
├── SOURCES
├── SPECS
└── SRPMS
```

首先在SOURCES目录创建一个名为Streamer-web-7.0.7的文件夹，将之前生成stmweb.jar放入其中，编写对应的service文件用于启动与停止服务：

```shell
[Unit]
Description=Starts and stops the stmweb daemon
After=network.target

[Service]
Type=simple
PIDFile=/var/run/stmwebd.pid
ExecStart=/usr/bin/java -jar /usr/local/stmweb/stmweb.jar
ExecStopPost=/bin/rm -f /var/run/stmwebd.pid

PrivateTmp=false

[Install]
WantedBy=multi-user.target
```

然后将Streamer-web-7.0.7文件夹打成tar.gz包，执行以下命令：

```shell
tar -zxvf Streamer-web-7.0.7.tar.gz Streamer-web-7.0.7
```

生成Streamer-web-7.0.7.tar.gz，此时rpmbuild目录结构：

```shell
rpmbuild/
|-- BUILD
|-- BUILDROOT
|-- RPMS
|-- SOURCES
|   |-- Streamer-web-7.0.7
|   |   |-- stmweb.jar
|   |   `-- stmweb.service
|   `-- Streamer-web-7.0.7.tar.gz
|-- SPECS
|-- SRPMS
```

然后编写spec文件，编写完的Streamer-7.0.7.spec如下：

```shell
Name: Streamer-web
Version:      7.0.7
Release:      1.infonix
Summary: Streamer 7
Group:infocore
License: Share
Source:	%{name}-%{version}.tar.gz
BuildRoot: %(mktemp -ud %{_tmppath}/%{name}-%{version}-%{release}-XXXXXX)

BuildRequires: java-1.8.0-openjdk-devel >= 1.8.0
Requires: java-1.8.0-openjdk >= 1.8.0

%description

%prep
%define __strip /bin/true
%define __os_install_post %{nil}

%setup -n %{name}-%{version}

%install
rm -rf %{buildroot}


%define _webhome /usr/local/stmweb

#directory for config file of stmweb service
%define _systemddir /usr/lib/systemd/system

mkdir -p %{buildroot}%{_webhome}
mkdir -p %{buildroot}%{_systemddir}

install -m 777 stmweb.jar %{buildroot}%{_webhome}
install -m 755 stmweb.service %{buildroot}%{_systemddir}
%clean
rm -rf %{buildroot}

%files
%defattr(-,root,root,-)
%{_webhome}/stmweb.jar
%{_systemddir}/stmweb.service

%post
/usr/bin/systemctl stop stmweb  >/dev/null 2>&1
if [ "$1" = "1" ]; then
	/sbin/ldconfig
	/usr/bin/systemctl enable stmweb >/dev/null 2>&1
fi
/usr/bin/systemctl daemon-reload
/usr/bin/systemctl start stmweb  >/dev/null 2>&1

%preun
if [ "$1" = "0" ]; then
	/usr/bin/systemctl stop stmweb  >/dev/null 2>&1
	/usr/bin/systemctl disable stmweb >/dev/null 2>&1
fi

%changelog
```

编写完成后根据spec文件执行得到对应的RPM包，需要注意要保证jdk的版>=1.8：

```shell
rpmbuild -bb Streamer-7.0.7.spec 
	或
rpmbuild -ba Streamer-7.0.7.spec 
```

生成完后的目录结构为：

```shell
rpmbuild/
|-- BUILD
|   `-- Streamer-web-7.0.7
|       |-- stmweb.jar
|       `-- stmweb.service
|-- BUILDROOT
|   |-- Streamer-web-7.0.7-1.infonix.aarch64
|   |   `-- usr
|   |       |-- lib
|   |       |   `-- systemd
|   |       |       `-- system
|   |       |           `-- stmweb.service
|   |       `-- local
|   |           `-- stmweb
|   |               `-- stmweb.jar
|   |-- Streamer-web-7.0.7-8.infonix.aarch64
|   |   `-- usr
|   |       |-- bin
|   |       |-- lib
|   |       |   `-- systemd
|   |       |       `-- system
|   |       |           `-- stmweb.service
|   |       `-- local
|   |           `-- stmweb
|   |               |-- lib
|   |               `-- stmweb.jar
|   `-- Streamer-web-7.0.7-9.infonix.aarch64%{_weblibdir}
|-- RPMS
|   `-- aarch64
|       |-- Streamer-web-7.0.7-1.infonix.aarch64.rpm
|-- SOURCES
|   |-- bak
|   |   |-- Streamer-web-7.0.7
|   |   |   |-- stmweb.jar
|   |   |   `-- stmweb.service
|   |   `-- Streamer-web-7.0.7.tar.gz
|   |-- Streamer-web-7.0.7
|   |   |-- stmweb.jar
|   |   `-- stmweb.service
|   |-- Streamer-web-7.0.7_bak
|   `-- Streamer-web-7.0.7.tar.gz
|-- SPECS
|   `-- Streamer-7.0.7.spec
`-- SRPMS
    |-- Streamer-web-7.0.7-1.infonix.src.rpm
```

最后我们制作完成RPM包了，通过下列命令安装：

```shell
rpm -ivh Streamer-web-7.0.7-1.infonix.aarch64.rpm
```

安装完成的RPM包会在/usr/local/stmweb/stmweb.jar存在jar包，我们启动RPM包实际上就是启动这个jar包，最后通过以下命令分别启动和停止服务：

```shell
systemctl status stmweb  #查看服务状态
systemctl start stmweb   #启动服务
systemctl stop stmweb    #停止服务
systemctl restart stmweb #重启服务
```

运行成功状态如下：

```shell
stmweb.service - Starts and stops the stmweb daemon
   Loaded: loaded (/usr/lib/systemd/system/stmweb.service; enabled; vendor preset: disabled)
   Active: active (running) since Sun 2020-02-02 09:56:56 CST; 1 weeks 0 days ago
 Main PID: 2082 (java)
   CGroup: /system.slice/stmweb.service
           └─2082 /usr/bin/java -jar /usr/local/stmweb/stmweb.jar
```

停止后状态如下：

```shell
stmweb.service - Starts and stops the stmweb daemon
   Loaded: loaded (/usr/lib/systemd/system/stmweb.service; enabled; vendor preset: disabled)
   Active: failed (Result: exit-code) since Sun 2020-02-09 14:32:37 CST; 1s ago
  Process: 16670 ExecStopPost=/bin/rm -f /var/run/stmwebd.pid (code=exited, status=0/SUCCESS)
  Process: 2082 ExecStart=/usr/bin/java -jar /usr/local/stmweb/stmweb.jar (code=exited, status=143)
 Main PID: 2082 (code=exited, status=143)
```



