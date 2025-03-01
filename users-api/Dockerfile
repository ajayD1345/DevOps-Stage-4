# Use an official Maven image to build the application
FROM maven:3.8.7-eclipse-temurin-17 AS builder

# Set the working directory inside the container
WORKDIR /app

# Copy the Maven wrapper and configuration
COPY pom.xml .
COPY mvnw .
COPY .mvn/ .mvn/

# Copy the source code
COPY src/ src/

# Make sure the Maven wrapper script is executable
RUN chmod +x mvnw

# Build the application
RUN mvn clean install -DskipTests

# Use a minimal JDK image for running the app
FROM eclipse-temurin:17-jdk-alpine

# Set the working directory
WORKDIR /app

# Copy the JAR file from the builder stage
COPY --from=builder /app/target/users-api-0.0.1-SNAPSHOT.jar users-api.jar

# Expose the API port
EXPOSE 8083

# Command to run the application
CMD ["java", "-jar", "users-api.jar"]
