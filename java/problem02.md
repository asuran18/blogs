>Caused by: 
org.xml.sax.SAXParseException; lineNumber: 60; columnNumber: 37; 必须声明元素类型 "package"。

###### 原因:
在mybatis-config.xml文件中

	<typeHandlers>
		<package name="com.mlp.web.util"/>
	</typeHandlers>

但是在之前的使用中并没有出现问题，对比之后发现，是jar包的问题。我之前使用的是`mybatis-3.3.0`的jar包，但移植到的项目中是`mybatis-3.0.4`的jar包，而在网上看到MyBtis在3.2以后才支持通过包名进行注解。

###### 解决方法：
1. 更新jar包
2. 按照旧版本的方式进行注解。

如：将`<package name="com.mlp.web.util"/>`
改为`<typeHandler javaType="list" jdbcType="VARCHAR" handler="com.mlp.web.utilJsonObjectHandler"/>`
