From gradle:9.4.1-jdk21-alpine AS builder
WORKDIR /app
COPY . .
RUN gradle clean build -x test --no-daemon

From eclipse-temurin:21-jre-alpine
WORKDIR /app
COPY --from=builder /app/build/libs/*.jar app.jar
EXPOSE 8089
ENTRYPOINT ["java", "-jar", "app.jar"]
