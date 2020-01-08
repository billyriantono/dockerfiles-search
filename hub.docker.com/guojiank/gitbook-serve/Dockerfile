FROM guojiank/gitbook-serve:base

COPY app.jar /app.jar
COPY gitbook-init.sh /gitbook-init.sh
COPY gitbook-serve.sh /gitbook-serve.sh

WORKDIR /gitbook

EXPOSE 4000
EXPOSE 8081

CMD ["java", "-jar", "/app.jar"]
