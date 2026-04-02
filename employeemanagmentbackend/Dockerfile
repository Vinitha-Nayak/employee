# -------- Build Stage --------
FROM maven:3.9.9-eclipse-temurin-17 AS build
WORKDIR /build

COPY . .
RUN mvn clean package -DskipTests

# -------- Runtime Stage --------
FROM eclipse-temurin:17-jdk-alpine
WORKDIR /app

RUN addgroup -S appgroup && adduser -S appuser -G appgroup

COPY --from=build /build/target/*.jar app.jar

RUN chown -R appuser:appgroup /app
USER appuser

EXPOSE 8080

ENTRYPOINT ["java","-jar","/app/app.jar"]
