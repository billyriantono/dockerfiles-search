FROM openjdk:8-jdk-alpine

RUN apk --update add --no-cache git && \ 
    wget -q -O - 'https://github.com/redpen-cc/redpen/releases/download/redpen-1.9.0/redpen-1.9.0.tar.gz' | tar -xz && \
    cp -av redpen-distribution-1.9.0/* /usr/local/ && \
    rm -rf redpen-distribution-1.9.0

CMD ["redpen", "-help"]
