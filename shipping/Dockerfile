### Stage 1: Build ###
FROM maven:3.9.11 AS build
WORKDIR /opt/server

# Copy code
COPY pom.xml .
COPY src ./src

# Build application and create JAR
RUN mvn clean package -DskipTests

### Stage 2: Runtime ###
FROM openjdk:17
WORKDIR /opt/server

# Copy the JAR from build stage
COPY --from=build /opt/server/target/shipping-1.0.jar shipping.jar

EXPOSE 8080

ENV CART_ENDPOINT="cart:8080" \
    DB_HOST="mysql"

# Run the app
CMD ["java", "-jar", "shipping.jar"]
