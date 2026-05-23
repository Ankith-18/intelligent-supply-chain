FROM maven:3.9.9-eclipse-temurin-21 AS build

WORKDIR /app

COPY shared-kafka-events ./shared-kafka-events
WORKDIR /app/shared-kafka-events
RUN mvn clean install -DskipTests

WORKDIR /app
COPY api-gateway ./api-gateway
WORKDIR /app/api-gateway
RUN mvn clean package -DskipTests

FROM eclipse-temurin:21-jre

WORKDIR /app
COPY --from=build /app/api-gateway/target/*.jar app.jar

EXPOSE 8080

ENTRYPOINT ["java","-jar","app.jar","--spring.profiles.active=prod"]