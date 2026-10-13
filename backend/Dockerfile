# Stage 1: Build the application
FROM maven:3.9.6-eclipse-temurin-17-alpine AS build
WORKDIR /app

# Copy settings.xml and source code
COPY settings.xml /root/.m2/settings.xml
COPY pom.xml .
COPY src ./src

# Build the application
RUN mvn clean package -DskipTests -B -s /root/.m2/settings.xml

# Stage 2: Run the application
FROM eclipse-temurin:17-jre-alpine
WORKDIR /app
COPY --from=build /app/target/*.jar app.jar

EXPOSE 8080

ENTRYPOINT ["java", "-Djava.net.preferIPv4Stack=true", "-jar", "app.jar"]
