# Use an official Maven image to build the application
FROM maven:3.8.7-eclipse-temurin-17 AS builder

# Set the working directory inside the container
WORKDIR /app

# Copy the project files
COPY . .

# Build the application
RUN ./mvnw clean install

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
