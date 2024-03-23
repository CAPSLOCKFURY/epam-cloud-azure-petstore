#
# Build stage
#
FROM maven:3.8.4-openjdk-17-slim AS build
WORKDIR /build
COPY pom.xml .
COPY src ./src
RUN mvn clean package

#
# Package stage
#
FROM openjdk:17-slim
COPY --from=build /build/target/*.jar /app/petstorepetservice.jar
COPY --from=build /build/src/main/resources/app-insights/applicationinsights-agent-3.5.0.jar /app/applicationinsights-agent.jar
EXPOSE 8080
ENTRYPOINT ["java","-javaagent:/app/applicationinsights-agent.jar","-jar","/app/petstorepetservice.jar"]
