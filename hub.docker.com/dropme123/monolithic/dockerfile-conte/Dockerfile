FROM adoptopenjdk/maven-openjdk8 AS build
WORKDIR /root
COPY . .
RUN mvn package
RUN ls -la target

FROM adoptopenjdk:11-jre-hotspot AS deploy
RUN mkdir /opt/app
COPY --from=build /root/target/*.jar /opt/app
CMD [ "java", "-jar", "/opt/app/wishlist-0.0.1-SNAPSHOT.jar" ]