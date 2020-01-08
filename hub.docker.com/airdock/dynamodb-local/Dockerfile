# VERSION 1.0
# AUTHOR:         Jerome Guibert <jguibert@gmail.com>
# DESCRIPTION:    dynamodb-local image based on oracle-jdk
# TO_BUILD:       docker build --rm -t airdock/dynamodb-local .
# SOURCE:         https://github.com/airdock-io/docker-dynamodb-local
FROM airdock/oracle-jdk:latest
LABEL maintainer Jerome Guibert <jguibert@gmail.com>

 RUN apt-get update -qq && apt-get install -y --no-install-recommends ca-certificates && \
  mkdir -p /opt/dynamodb-local && mkdir -p /srv/dynamodb-local && \
  curl -L http://dynamodb-local.s3-website-us-west-2.amazonaws.com/dynamodb_local_latest.tar.gz | tar xvzf - -C /opt/dynamodb-local && \
  chown -R java:java /opt/dynamodb-local && chown -R java:java /srv/dynamodb-local

EXPOSE 8000

WORKDIR /opt/dynamodb-local

CMD ["gosu", "java:java", "java" , "-Djava.library.path=/opt/dynamodb-local/DynamoDBLocal_lib" , "-jar", "/opt/dynamodb-local/DynamoDBLocal.jar", "-sharedDb", "--dbPath", "/srv/dynamodb-local"]
