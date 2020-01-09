ARG VERSION=8
FROM openjdk:${VERSION}-jdk-slim AS build 
COPY . /src
WORKDIR /src
RUN ./gradlew --no-daemon build

FROM openjdk:${VERSION}-jre-alpine AS runtime 
ARG APP_NAME=template
USER nobody
COPY --from=build /src/build/libs/${APP_NAME}.jar /app/app.jar

WORKDIR /app
CMD ["java","-jar","app.jar"]
