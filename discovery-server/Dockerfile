FROM maven:3.9.9-eclipse-temurin-21 AS build

WORKDIR /app

COPY shared-kafka-events ./shared-kafka-events
WORKDIR /app/shared-kafka-events
RUN mvn clean install -DskipTests

WORKDIR /app
COPY discovery-server ./discovery-server
WORKDIR /app/discovery-server
RUN mvn clean package -DskipTests

FROM eclipse-temurin:21-jre

WORKDIR /app
COPY --from=build /app/discovery-server/target/*.jar app.jar

EXPOSE 8761

ENTRYPOINT ["java","-jar","app.jar","--spring.profiles.active=prod"]