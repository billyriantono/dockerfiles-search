FROM onema/scala-sbt:8u171-2.12.6-1.2.1-build

RUN apk add --update nodejs && \
    apk add npm && \
    npm install -g serverless && \
    pip install --upgrade awscli

VOLUME /root/app
