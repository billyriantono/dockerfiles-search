From docker:latest

RUN mkdir /root/.docker
Add config.json /root/.docker/config.json
RUN apk add --no-cache git make go musl-dev && \
    go get -u github.com/awslabs/amazon-ecr-credential-helper/ecr-login/cli/docker-credential-ecr-login && \
    cp /root/go/bin/docker-credential-ecr-login /bin/ && \
    rm -Rf /root/go && \
    apk del --purge nghttp2-libs libssh2 libcurl expat pcre2 git binutils gmp isl libgomp libatomic pkgconf libgcc mpfr3 mpc1 libstdc++ gcc go make musl-dev
