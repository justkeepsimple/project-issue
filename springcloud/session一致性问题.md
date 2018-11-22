利用redis来实现session一致性问题

各微服务加入maven依赖

 <!--redis-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-redis</artifactId>
        </dependency>

        <!-- redis实现session一致 -->
        <dependency>
            <groupId>org.springframework.session</groupId>
            <artifactId>spring-session-data-redis</artifactId>
        </dependency>
        
        
        启动类加上@EnableRedisHttpSession注解
        
        
        zuul网关同样配置
        
        通过zuul网关调用时，发现session不一致
        
        在zuul网关中设置全局变量
        
        zuul.sensitive-headers="*"
        
        
        启动网关服务时报错  *不是指定的字符集
        
        将*转为ASCII 码即可 \u002a
