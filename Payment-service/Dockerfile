FROM maven:3.9.9-eclipse-temurin-21 AS build

WORKDIR /app

COPY shared-kafka-events ./shared-kafka-events
WORKDIR /app/shared-kafka-events
RUN mvn clean install -DskipTests

WORKDIR /app
COPY Payment-service ./Payment-service
WORKDIR /app/Payment-service
RUN mvn clean package -DskipTests

FROM eclipse-temurin:21-jre

WORKDIR /app
COPY --from=build /app/Payment-service/target/*.jar app.jar

EXPOSE 9050

ENTRYPOINT ["java","-jar","app.jar","--spring.profiles.active=prod"]