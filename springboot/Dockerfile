FROM eclipse-temurin:17-jdk-alpine
VOLUME /tmp

### all you need to copy over is the compiled jar file!
COPY ./target/*.jar app.jar
CMD ["java","-jar","/app.jar"]