FROM lwieske/java-8
MAINTAINER Alexander Lukyanchikov <sqshq@sqshq.com>

ADD ./target/demo-config.jar /app/
CMD ["java", "-Xmx200m", "-jar", "/app/demo-config.jar"]

EXPOSE 8888
