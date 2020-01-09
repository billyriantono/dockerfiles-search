FROM debian:stretch AS compiler
RUN apt-get -y update
RUN apt-get install -y build-essential
COPY hello.c /
RUN make hello
FROM debian:stretch
COPY --from=compiler /hello /hello
CMD /hello
