FROM maven:3.9.9-eclipse-temurin-21 AS build

WORKDIR /app

COPY . .

WORKDIR /app/shared-kafka-events
RUN mvn clean install -DskipTests

WORKDIR /app/return-service
RUN mvn clean package -DskipTests


FROM eclipse-temurin:21-jre

WORKDIR /app

COPY --from=build /app/return-service/target/*.jar app.jar

EXPOSE 9080

ENTRYPOINT ["java", "-jar", "app.jar", "--spring.profiles.active=prod"]