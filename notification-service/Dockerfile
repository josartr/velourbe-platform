FROM gradle:9.4.1-jdk21-alpine AS builder
WORKDIR /app
COPY . .
RUN gradle clean build -x test --no-daemon

FROM eclipse-temurin:21-jre-alpine
WORKDIR /app
COPY --from=builder /app/build/libs/*.jar app.jar
EXPOSE 8085
HEALTHCHECK --interval=30s --timeout=10s --start-period=40s --retries=3 \
    CMD java -jar app.jar || exit 1
ENTRYPOINT ["java", "-jar", "app.jar"]
