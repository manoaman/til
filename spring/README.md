### Spring stuffs

#### How to specify which profile to use in a test class?

`SomeTest.java`

```
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration(locations={"classpath:**/test-applicationContext.xml"})
@ActiveProfiles("development")
```

`test-applicationContext.xml`
```
  	<beans profile="development">
    	<context:property-placeholder ignore-resource-not-found="true" location="classpath:**/development.properties" />
  	</beans>
    
	<bean class="org.apache.commons.dbcp.BasicDataSource" destroy-method="close" id="dataSource">
		<property name="driverClassName"><value>${jdbc.driver}</value></property>
        <property name="url"><value>${jdbc.url}</value></property>
        <property name="username"><value>${jdbc.username}</value></property>
        <property name="password"><value>${jdbc.password}</value></property>
        <property name="maxActive"><value>${jdbc.maxactive}</value></property>
    </bean>    
```

`development.properties`

```
jdbc.driver=com.mysql.jdbc.Driver
jdbc.url=jdbc:mysql://localhost:3306/somedb?zeroDateTimeBehavior=convertToNull
jdbc.username=xxx
jdbc.password=xxxx
jdbc.maxactive=10
```

and this will refer to `development.properties`
