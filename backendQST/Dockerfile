# Use an official Maven image to build the project
FROM maven:3.8.6-openjdk-17 AS build

# Set the working directory inside the container
WORKDIR /app

# Copy only necessary files for dependency caching
COPY pom.xml .
COPY mvnw .

# Download dependencies to cache them
RUN mvn dependency:go-offline

# Copy the entire source code and build the application
COPY src src
RUN mvn clean package -DskipTests

# Use a smaller JDK runtime image for the final build
FROM eclipse-temurin:17-jdk-jammy

# Set the working directory in the container
WORKDIR /app

# Copy the JAR file from the builder stage
COPY --from=build /app/target/*.jar app.jar

# Expose the application port
EXPOSE 8080

# Run the application
ENTRYPOINT ["java", "-jar", "app.jar"]
