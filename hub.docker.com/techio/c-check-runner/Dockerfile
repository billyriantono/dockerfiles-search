FROM gcc:6.3

COPY entrypoint.sh /
COPY build.sh /project/build

RUN apt-get update && apt-get install -y check

ENTRYPOINT ["/entrypoint.sh"]
