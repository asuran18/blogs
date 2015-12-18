>org.springframework.jdbc.UncategorizedSQLException: SqlSession operation;
 uncategorized SQLException for SQL []; 
 SQL state [25006]; 
 error code [0]; 
 错误: 不能在一个只读模式的事务中执行INSERT; 

###### 原因：
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

###### 解决方法：

1. 修改方法前缀名，如add/save等已被配置过的前缀
2. 为该前缀添加配置。在事务配置中添加一行：
`<tx:method name="create*" propagation="REQUIRED" rollback-for="java.lang.Exception" />`
