## Maven Site Plugin 介绍
> 使用maven-site-plugin，在site是生成一个静态站点，反应各种信息。

### 简单实践
```xml
<build>  
    <pluginManagement>  
        <plugins>               
        <!-- 构建项目站点报告插件-->  
            <plugin>  
                <groupId>org.apache.maven.plugins</groupId>  
                <artifactId>maven-site-plugin</artifactId>  
                <version>3.4</version>  
                <configuration>  
                </configuration>  
            </plugin>  
        </plugins>  
    </pluginManagement>  
</build>  
```

执行
``` java
mvn clean site  
```
在target中生成静态html文件，可查看报告。


### Project Report Plugins

|GroupId                    | ArtifactId                        |Version    |
|---------------------------|-----------------------------------|-----------|
|org.apache.maven.plugins   |maven-checkstyle-plugin 	        |2.15       |
|org.apache.maven.plugins   |maven-invoker-plugin 	            |2.0.0      |
|org.apache.maven.plugins   |maven-javadoc-plugin 	            |2.9.1      |
|org.apache.maven.plugins   |maven-jxr-plugin 	                |2.5        |
|org.apache.maven.plugins   |maven-plugin-plugin 	            |3.4        |
|org.apache.maven.plugins   |maven-pmd-plugin 	                |3.5        |
|org.apache.maven.plugins   |maven-project-info-reports-plugin 	|2.8.1      |
|org.apache.maven.plugins   |maven-surefire-report-plugin 	    |2.18.1     |
|org.codehaus.mojo 	        |findbugs-maven-plugin 	            |2.5.5      |
|org.codehaus.mojo 	        |l10n-maven-plugin 	                |1.0-alpha-2|
|org.codehaus.mojo 	        |taglist-maven-plugin 	            |2.4        |
|org.codehaus.sonar-plugins |maven-report 	                    |0.1        |