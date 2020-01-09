FROM ubuntu

RUN apt-get update && apt-get install -y build-essential python python3

COPY ./framework/ /framework

RUN echo "#!/bin/sh" > /build && chmod +x /build
COPY ./docker_run.sh /test
RUN chmod +x /test
CMD ["/test"]
