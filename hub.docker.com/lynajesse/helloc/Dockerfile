FROM ubuntu
RUN apt-get update && apt-get install -y build-essential
WORKDI /hello
RUN apt-get install -y build-essential
COPY hello.c ./
RUN make hello
run apt -y remove build-essential && apt -y autoremove && rm -rf /var/lib/apt
CMD /hello

