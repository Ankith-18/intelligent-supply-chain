
FROM maven:3.9.9-eclipse-temurin-21 AS build
WORKDIR /app

COPY . .


WORKDIR /app/shared-kafka-events
RUN mvn clean install -DskipTests

WORKDIR /app/Inventory-service
RUN mvn clean package -DskipTests

FROM eclipse-temurin:21-jre

WORKDIR /app
COPY --from=build /app/Inventory-service/target/*.jar app.jar

EXPOSE 9030

ENTRYPOINT ["java", "-jar", "app.jar", "--spring.profiles.active=prod"]