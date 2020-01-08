FROM bankmonitor/spring-boot:latest
WORKDIR /app
CMD ["bash", "-c", "env > application.properties; java $JAVA_OPTS -jar /app/app.jar --spring.profiles.active=$SPRING_PROFILES_ACTIVE"]