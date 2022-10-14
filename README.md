java -javaagent:opentelemetry-javaagent.jar  -jar target/*.jar

export OTEL_EXPORTER_ZIPKIN_ENDPOINT=http://localhost:9411/api/v2/spans
export OTEL_TRACES_EXPORTER=zipkin
export OTEL_SERVICE_NAME=front-service


		<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-sleuth-zipkin</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-starter-sleuth</artifactId>
		</dependency>


server.port: 8081

spring:
application:
name: customer-service

zipkin:
baseUrl: http://localhost:9411

sleuth:
sampler:
probability: 1.0 # allowed values between 0.0 - 0.1