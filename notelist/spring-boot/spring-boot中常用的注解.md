## spring-boot中常用的注解



注解        | 作用          | 
--------------------|------------------|
@Configuration| 作用于类上，相当于一个 xml 配置文件  | 
@Bean|  作用于方法上，相当于 xml 配置中的 <bean> | 
@SpringBootApplication |  Spring Boot的核心注解，是一个组合注解，用于启动类上  | 
@EnableAutoConfiguration  	| 启用自动配置，允许加载第三方 Jar 包的配置  | 
@ComponentScan   |默认扫描 @SpringBootApplication 所在类的同级目录以及它的子目录   | 
@PropertySource   |  加载 properties 文件 | 
@Value | 将配置文件的属性注入到 Bean 中特定的成员变量  | 
@EnableConfigurationProperties | 开启一个特性，让配置文件的属性可以注入到 Bean 中，与 @ConfigurationProperties 结合使用|
@ConfigurationProperties   | 关联配置文件中的属性到 Bean 中|
@Import  |加载指定 Class 文件，其生命周期被 Spring 管理 |
@ImportResource    |加载 xml 文件 |
