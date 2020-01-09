FROM haskell:8.6.5

# Install dependecies needed to compile Haskell libraries
RUN apt-get update \
    && apt-get install --yes xz-utils make unzip \
    && apt-get clean

RUN stack --resolver lts-14.7 install base \
    protolude \
    text \
    aeson \
    yaml \
    unordered-containers \
    case-insensitive \
    regex-compat \
    wai \
    warp \
    diagrams \
    proto-lens \
    proto-lens-setup \
    proto-lens-runtime \
    proto-lens-protoc 

RUN curl -L https://github.com/protocolbuffers/protobuf/releases/download/v3.10.0/protoc-3.10.0-linux-x86_64.zip > protoc.zip \
&& unzip protoc.zip -d /usr/local \
&& cp -rf /root/.local/bin/* /usr/local/bin/ \
&& rm -rf protoc.zip

