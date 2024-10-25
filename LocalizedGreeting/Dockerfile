# Stage 1: Build the application with JDK 17
FROM maven:3.8.4-openjdk-17 AS build

# Set the working directory
WORKDIR /app

# Copy the pom.xml and source files
COPY pom.xml .
COPY src ./src

# Build the application
RUN mvn clean package -DskipTests -X

# Stage 2: Create a smaller runtime image
FROM openjdk:17-jre-slim

# Set the working directory
WORKDIR /app

# Copy only the JAR file from the build stage
COPY --from=build /app/target/*.jar app.jar

# Command to run the application
ENTRYPOINT ["java", "-jar", "app.jar"]
