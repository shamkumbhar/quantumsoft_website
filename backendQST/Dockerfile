# Use an official Maven image to build the project
FROM maven:latest
WORKDIR /app
COPY pom.xml .
COPY mvnw .

RUN mvn dependency:go-offline
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
