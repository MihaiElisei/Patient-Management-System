# ===== Build stage =====
FROM maven:3.9.9-eclipse-temurin-21 AS builder
WORKDIR /app

# Copy pom.xml first to cache dependencies
COPY pom.xml .

# Download dependencies for offline use
RUN mvn dependency:go-offline -B

# Copy source code
COPY src ./src

# Build the jar
RUN mvn clean package -DskipTests -B

# ===== Run stage =====
FROM eclipse-temurin:21-jre AS runner
WORKDIR /app

# Copy the built jar
COPY --from=builder /app/target/analytics-service-0.0.1-SNAPSHOT.jar ./app.jar

EXPOSE 4002

ENTRYPOINT ["java", "-jar", "app.jar"]
