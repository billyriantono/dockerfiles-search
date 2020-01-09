FROM hakhak/ubuntu:compile
ADD https://raw.githubusercontent.com/herveleclerc/tutodockeraw/master/add/hello_add.c /
RUN make hello_add && rm -f /hello_add.c
CMD /hello_add
