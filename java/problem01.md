
>Caused by: 
java.lang.AbstractMethodError: 
org.mybatis.spring.transaction.SpringManagedTransactionFactory.newTransaction(Ljava/sql/Connection;)Lorg/apache/ibatis/transaction/Transaction; 

###### 解决方法：
mybatis-spring-1.0.0-RC2.jar版本不对，换成较新版本即可
