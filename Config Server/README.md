Spring Cloud Config Server:

Every Microservice will have dev, uat, prod etc environments. Therefore, every microservice will have min 3 properties files. And there can be 100's of Microservices which will form a Web site. So, there will be 100*3 = 300 properties files. Inorder to manage all of them in one place and make things easy Spring Cloud Config Server came into picture.

1) All the Microservices connect to Spring Cloud Config Server
2) Config Server connects to a git repository location
3) Git repository contains all the properties files of all microservices committed.

Steps to set up Spring Cloud Config Server:

1) Create a new Spring Boot application and add 'Config Server' dependency in the same.
2) Along with @SpringBootApplication, add <b>@EnableConfigServer.</b>
3) Create a git local repository using command prompt and commit all the properties files to local repository with file names like {applicationName}-{environment}.properties.
4) Connect the Config Server to git local repository by giving <b>local file path of git repository in application.properties file of Config server.</b>

ex: spring.cloud.config.server.git.uri=file:///D:/workspace practice/microservices/Config Server/git-localconfig-repo

Note: 1) Properties files must be committed to git local repository for them to be picked up.
      2) Use config server url: localhost:{port}/{applicationName}/{environment} to see the properties.
      
Steps to connect Microservices to Config Server:

1) Rename application.properties to bootstrap.properties.
2) Connect each microservice to Config Server by providing config server url in bootstrap.properties.
ex: spring.cloud.config.uri=http://localhost:8888 (This is url of Config Server.)
      

