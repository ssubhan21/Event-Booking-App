# build stage
FROM gradle:8-jdk22-alpine AS builder

COPY --chown=gradle .. /home/gradle/src
# Set the working directory
WORKDIR /home/gradle/src/

RUN gradle build -x test

#package stage
FROM openjdk:22-jdk

RUN mkdir /app

COPY --from=builder /home/gradle/src/build/libs/*.jar /app/booking-service.jar


ENV MONGO_DB_USERNAME=admin \
    MONGO_DB_PWD=password

EXPOSE 8093

ENTRYPOINT ["java","-jar", "/app/booking-service.jar"]