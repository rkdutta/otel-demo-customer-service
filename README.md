# Customer Service
#### simulating 3rd party backend api


### Execute 
```
mvn spring-boot:run
```


## Enable OpenTelemetry

1. Add the following dependencies in [pom.xml](pom.xml)
```xml
		<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-sleuth-zipkin</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-starter-sleuth</artifactId>
		</dependency>
```

2. Add/append the following in [application.yml](/src/main/resources/application.yml)

```yaml
server.port: 8081

spring:
    application:
        name: customer-service
    zipkin:
        baseUrl: http://localhost:9411
    sleuth:
        sampler:
            probability: 1.0 # allowed values between 0.0 - 0.1
```

3. Start a zipkin server using Docker
```
docker network create tracing
docker run -d --rm -it --name zipkin --network tracing -p 9411:9411 openzipkin/zipkin:latest
```

4. Restart the service
```
mvn spring-boot:run
```

## Instrumenting by injecting agent during startup
```
export OTEL_EXPORTER_ZIPKIN_ENDPOINT=http://localhost:9411/api/v2/spans
export OTEL_TRACES_EXPORTER=zipkin
export OTEL_SERVICE_NAME=front-service
java -javaagent:opentelemetry-javaagent.jar  -jar target/*.jar
```


