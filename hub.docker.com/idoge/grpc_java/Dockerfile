FROM idoge/grpcpp:latest AS build-env


COPY pkgs-install.sh /root/docker/
RUN bash -ex /root/docker/pkgs-install.sh


FROM idoge/grpcpp:latest
LABEL version="1.0" \
    description="Centos7 grpc java suite" \
    by="doge.py" \
    maintainer="doge.py@gmail.com"

COPY --from=build-env /var/local/git/grpc-java/compiler/build/exe/java_plugin/protoc-gen-grpc-java /usr/local/bin/grpc_java_plugin
