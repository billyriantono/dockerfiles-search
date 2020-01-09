FROM cogniteev/oracle-java:java8

RUN apt-get update && \
    apt-get install -y curl && \
    apt-get install -y python-setuptools && \
    easy_install j2cli && \
    apt-get purge -y --auto-remove && rm -rf /var/lib/apt/lists/*

CMD ["java", "-version"]
