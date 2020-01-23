FROM lwieske/java-8
MAINTAINER Alexander Lukyanchikov <sqshq@sqshq.com>

ADD ./target/demo-spring-boot-admin.jar /app/
CMD ["java", "-Xmx200m", "-jar", "/app/demo-spring-boot-admin.jar"]

EXPOSE 8080
