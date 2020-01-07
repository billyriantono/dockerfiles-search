FROM stackmachine/protobuf:3.2.0

# install protobuf from source
RUN apt-get update && \
    apt-get install -y curl git build-essential autoconf libtool
RUN git clone --branch v1.2.3 https://github.com/grpc/grpc && \
    cd grpc && \
    git submodule update --init && \
    make && \
    make install && \
    cd .. && rm -rf grpc
RUN curl -o grpc_java_plugin -L 'http://search.maven.org/remotecontent?filepath=io/grpc/protoc-gen-grpc-java/1.2.0/protoc-gen-grpc-java-1.2.0-linux-x86_64.exe' && \
    chmod +x grpc_java_plugin && \
    mv grpc_java_plugin /usr/local/bin
