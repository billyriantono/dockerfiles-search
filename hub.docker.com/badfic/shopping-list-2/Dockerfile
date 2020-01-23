FROM openjdk:11-jdk-slim as build

ADD . /usr/share/shopping-list-build

WORKDIR /usr/share/shopping-list-build

RUN chmod +x gradlew && ./gradlew build

FROM openjdk:11-jre-slim
WORKDIR /usr/share/shopping-list

COPY --from=build /usr/share/shopping-list-build/build/libs/shoppinglist-0.0.1.jar .

EXPOSE 8080
ENTRYPOINT ["java", "-jar", "shoppinglist-0.0.1.jar"]