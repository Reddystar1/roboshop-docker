### Stage 1: Build ###
FROM maven:3.9.11 AS build
WORKDIR /opt/server

# Copy code
COPY pom.xml .
COPY src ./src

# Build application
RUN mvn clean package -DskipTests

### Stage 2: Runtime ###
FROM eclipse-temurin:17-jre
WORKDIR /opt/server

# Copy built JAR from stage 1
COPY --from=build /opt/server/target/shipping-1.0.jar shipping.jar

EXPOSE 8080

ENV CART_ENDPOINT="cart:8080" \
    DB_HOST="mysql"

CMD ["java", "-jar", "shipping.jar"]
