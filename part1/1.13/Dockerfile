FROM openjdk:8-slim


COPY spring-example-project /mydir/spring-example-project  
WORKDIR /mydir/spring-example-project  
RUN ./mvnw package  
CMD java -jar ./target/docker-example-1.1.3.jar
