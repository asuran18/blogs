### P1 ###
>Caused by: 
java.lang.AbstractMethodError: 
org.mybatis.spring.transaction.SpringManagedTransactionFactory.newTransaction(Ljava/sql/Connection;)Lorg/apache/ibatis/transaction/Transaction; 

######解决方法：
mybatis-spring-1.0.0-RC2.jar版本不对，换成较新版本即可

### P2 ###
>Caused by: 
org.xml.sax.SAXParseException; lineNumber: 60; columnNumber: 37; 必须声明元素类型 "package"。

######原因:
在mybatis-config.xml文件中

	<typeHandlers>
		<package name="com.mlp.web.util"/>
	</typeHandlers>

但是在之前的使用中并没有出现问题，对比之后发现，是jar包的问题。我之前使用的是`mybatis-3.3.0`的jar包，但移植到的项目中是`mybatis-3.0.4`的jar包，而在网上看到MyBtis在3.2以后才支持通过包名进行注解。

######解决方法：
1. 更新jar包
2. 按照旧版本的方式进行注解。

如：将`<package name="com.mlp.web.util"/>`
改为`<typeHandler javaType="list" jdbcType="VARCHAR" handler="com.mlp.web.utilJsonObjectHandler"/>`

### P3 ###
>org.springframework.jdbc.UncategorizedSQLException: SqlSession operation;
 uncategorized SQLException for SQL []; 
 SQL state [25006]; 
 error code [0]; 
 错误: 不能在一个只读模式的事务中执行INSERT; 

######原因：
 servise中的方法名为`createGroup`,
 在Spring的配置中，对transaction的配置为：

	 <tx:advice id="transactionAdvice" transaction-manager="transactionManager">
		<tx:attributes>
			<tx:method name="save*" propagation="REQUIRED"
				rollback-for="java.lang.Exception" />
			<tx:method name="add*" propagation="REQUIRED" rollback-for="java.lang.Exception" />
			<tx:method name="delete*" propagation="REQUIRED"
				rollback-for="java.lang.Exception" />
			<tx:method name="update*" propagation="REQUIRED"
				rollback-for="java.lang.Exception" />
			<tx:method name="insert*" propagation="REQUIRED"
				rollback-for="java.lang.Exception" />
			<tx:method name="remove*" propagation="REQUIRED"
				rollback-for="java.lang.Exception" />
			<tx:method name="get*" read-only="true" />
			<tx:method name="load*" read-only="true" />
			<tx:method name="find*" read-only="true" />
			<tx:method name="*" read-only="true" />
		</tx:attributes>
	</tx:advice>
	<aop:config>
		<aop:advisor pointcut="execution(* com.mlp.web.service..*.*(..))"
			advice-ref="transactionAdvice" />
	</aop:config>

执行createGroup方法时，因为事务的配置中没有以`create`为前缀的配置，而存在`<tx:method name="*" read-only="true" />`配置，所以默认该方法处于只读模式的事务中。

######解决方法：

1. 修改方法前缀名，如add/save等已被配置过的前缀
2. 为该前缀添加配置。在事务配置中添加一行：
`<tx:method name="create*" propagation="REQUIRED" rollback-for="java.lang.Exception" />`
