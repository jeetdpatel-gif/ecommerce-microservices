# Stage 1: Build the JAR
FROM maven:latest AS build
WORKDIR /home/app
COPY . .
# This creates the JAR inside the container's /home/app/target folder
RUN mvn clean package -DskipTests

# Stage 2: Create the final lean image
FROM eclipse-temurin:21-jre-jammy
WORKDIR /home/app
# Copy only the JAR from the 'build' stage
COPY --from=build /home/app/target/product-service-0.0.1-SNAPSHOT.jar .
EXPOSE 8888
ENTRYPOINT ["java", "-jar", "product-service-0.0.1-SNAPSHOT.jar"]
CMD ["mvn", "spring-boot:run"]