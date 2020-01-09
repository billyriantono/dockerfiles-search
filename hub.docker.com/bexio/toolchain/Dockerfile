FROM bexio/base:latest

EXPOSE 8080 8081 9000 9001 9999 10000 35729 35730
ENTRYPOINT ["/usr/local/bin/toolchain-exec"]
CMD ["/bin/bash", "-il"]

ADD . /tmp/toolchain.install.d
RUN /tmp/toolchain.install.d/install.sh
