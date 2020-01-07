FROM openjdk:alpine

LABEL maintainer="kterada.0509sg@gmail.com"
EXPOSE 8080

RUN set -x \
    # System update
    && apk --update add curl tar \
    # Create Directory
    && mkdir -p /usr/local/dynamodb-local \
    && cd /usr/local/dynamodb-local \
    # Get dynamodb local file & Decompression
    && curl -LOs http://dynamodb-local.s3-website-us-west-2.amazonaws.com/dynamodb_local_latest.tar.gz \
    && tar zxvf dynamodb_local_latest.tar.gz \
    # Create Database directory
    && mkdir -p /usr/local/dynamodb-local/db \
    # Remove Download File & cache
    && rm -rf /var/cache/apk/* dynamodb_local_latest.tar.gz

CMD ["java", "-Djava.library.path=/usr/local/dynamodb-local/DynamoDBLocal_lib", "-jar", "/usr/local/dynamodb-local/DynamoDBLocal.jar", "-port", "8080", "-dbPath", "/usr/local/dynamodb-local/db"]

