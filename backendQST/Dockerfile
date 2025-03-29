# Use an official Maven image to build the project
FROM eclipse-temurin:17-jdk-jammy
# Set the working directory in the container
WORKDIR /app
# Copy the JAR file from the builder stage
COPY /app/target/*.jar app.jar
# Expose the application port
EXPOSE 8080
# Run the application
ENTRYPOINT ["java", "-jar", "app.jar"]
