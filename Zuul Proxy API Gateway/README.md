<b>Zuul Proxy API Gateway:</b>

In Microservices architecture, there will be 100s of microservices and there are some common features that we have to implement for all these microservices like :
1) Authentication, Authorization and Security (It is required for each call to every microservice)
2) Fault Tolerance
3) Service Aggregation
4) Logging
5) Response Caching
6) Rate Limits (We can limit no. of requests to any particular microservice per sec or min.)

These are some features that can be done in API gateway.These are a great place for debugging and doing analytics.

  Any request to any API (From UI to APIs or from service to service) should pass through this first and then this API Gateway routes the request to the appropriate API based on the URL used to hit it. It intercepts all the requests to APIs and provide some services via filters.

<b>Steps to create a Zuul API Gateway:</b>
1) Create a seperate Spring Boot application for it.
2) Decide what should it do when it intercepts a request.

1) a. Create a spring boot application and add dependency in pom.xml and <b>make sure it is a eureka client.</b>
   b. Add @EnableZuulProxy on main() method containing @SpringBootApplication.

2) Define a custom Filter class extending <b>ZuulFilter</b> class. (This tells Zuul what to do when a request hits it ex: Logging, check authentication etc.)

<b>How to hit Zuul API Gateway and how Zuul hits correct API using URL:</b>

We have made Zuul API Gateway an Eureka Client, which means it registers with Eureka Naming Server just like other microservices. <b>Now, Zuul API Gateway grabs (dynamically) all the registry details of all the microservices registered with Eureka Naming Server.</b>

URL to hit Zuul API: http://localhost:8765/{ApplicationName}/{URI}

ex: http://localhost:8765/currency-conversion-service/currency-converter/from/USD/to/INR/quantity/10

<b>This url hits Zuul API as localhost:8765 is its address and executes any filters (Logging or Authentication) and then it gets the address of the microservice it has to hit from Eureka Naming Server registry details by matching {ApplicationName} and then the {URI} directs it to exact API endpoint.</b>

Similar thing happens every time it intercepts the calls between microservices. Only change is Let's say Mic A is calling Mic B, and Mic A has Zuul API Server Name in it, then it gets the address of Zuul API from Eureka and then use that to hit Zuul Gateway and route the call to appropriate API end point.


