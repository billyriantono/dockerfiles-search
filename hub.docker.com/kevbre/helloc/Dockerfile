FROM ubuntu
RUN apt-get update
RUN apt-get install -y build-essential
WORKDIR /hello
COPY hello.c /hello/
RUN make hello
CMD ./hello
