FROM alpine:3.9
LABEL maintainer="Lukas f. Paluch <fluktuid@gmail.com>"

RUN apk update
RUN apk add texlive-full=20170524-r6
RUN apk add ca-certificates=20190108-r0

VOLUME ["/source"]
WORKDIR /source
CMD ["bash"]
