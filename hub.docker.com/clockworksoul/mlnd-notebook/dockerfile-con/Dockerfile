FROM docker:17.12.0-ce as static-docker-source

FROM alpine:3.8 as protoc_builder
RUN apk add --no-cache build-base curl automake autoconf libtool git zlib-dev

ENV GRPC_VERSION=1.16.0 \
        GRPC_JAVA_VERSION=1.16.1 \
        GRPC_WEB_VERSION=1.0.0 \
        PROTOBUF_VERSION=3.6.1 \
        PROTOBUF_C_VERSION=1.3.1 \
        PROTOC_GEN_DOC_VERSION=1.1.0 \
        OUTDIR=/out
RUN mkdir -p /protobuf && \
        curl -L https://github.com/google/protobuf/archive/v${PROTOBUF_VERSION}.tar.gz | tar xvz --strip-components=1 -C /protobuf
RUN git clone --depth 1 --recursive -b v${GRPC_VERSION} https://github.com/grpc/grpc.git /grpc && \
        rm -rf grpc/third_party/protobuf && \
        ln -s /protobuf /grpc/third_party/protobuf
RUN mkdir -p /grpc-java && \
        curl -L https://github.com/grpc/grpc-java/archive/v${GRPC_JAVA_VERSION}.tar.gz | tar xvz --strip-components=1 -C /grpc-java
RUN mkdir -p /grpc-web && \
        curl -L https://github.com/grpc/grpc-web/archive/${GRPC_WEB_VERSION}.tar.gz | tar xvz --strip-components=1 -C /grpc-web
RUN mkdir -p /protobuf-c && \
        curl -L https://github.com/protobuf-c/protobuf-c/releases/download/v${PROTOBUF_C_VERSION}/protobuf-c-${PROTOBUF_C_VERSION}.tar.gz | tar xvz --strip-components=1 -C /protobuf-c
RUN cd /protobuf && \
        autoreconf -f -i -Wall,no-obsolete && \
        ./configure --prefix=/usr --enable-static=no && \
        make -j2 && make install
RUN cd grpc && \
        make -j2 plugins
RUN cd /grpc-java/compiler/src/java_plugin/cpp && \
        g++ \
        -I. -I/protobuf/src \
        *.cpp \
        -L/protobuf/src/.libs \
        -lprotoc -lprotobuf -lpthread --std=c++0x -s \
        -o protoc-gen-grpc-java
RUN cd /protobuf-c && \
        ./configure --prefix=/usr && \
        make -j2
RUN cd /protobuf && \
        make install DESTDIR=${OUTDIR}
RUN cd /grpc && \
        make install-plugins prefix=${OUTDIR}/usr
RUN cd /grpc-java/compiler/src/java_plugin/cpp && \
        install -c protoc-gen-grpc-java ${OUTDIR}/usr/bin/
RUN cd /grpc-web/javascript/net/grpc/web && \
        make && \
        install protoc-gen-grpc-web ${OUTDIR}/usr/bin/
RUN cd /protobuf-c && \
        make install DESTDIR=${OUTDIR}
RUN find ${OUTDIR} -name "*.a" -delete -or -name "*.la" -delete

RUN apk add --no-cache go
ENV GOPATH=/go \
        PATH=/go/bin/:$PATH
RUN go get -u -v -ldflags '-w -s' \
        github.com/Masterminds/glide \
        github.com/golang/protobuf/protoc-gen-go \
        github.com/gogo/protobuf/protoc-gen-gofast \
        github.com/gogo/protobuf/protoc-gen-gogo \
        github.com/gogo/protobuf/protoc-gen-gogofast \
        github.com/gogo/protobuf/protoc-gen-gogofaster \
        github.com/gogo/protobuf/protoc-gen-gogoslick \
        github.com/twitchtv/twirp/protoc-gen-twirp \
        github.com/chrusty/protoc-gen-jsonschema \
        github.com/grpc-ecosystem/grpc-gateway/protoc-gen-swagger \
        github.com/grpc-ecosystem/grpc-gateway/protoc-gen-grpc-gateway \
        github.com/johanbrandhorst/protobuf/protoc-gen-gopherjs \
        github.com/ckaznocha/protoc-gen-lint \
        github.com/mwitkow/go-proto-validators/protoc-gen-govalidators \
        github.com/lyft/protoc-gen-validate \
        moul.io/protoc-gen-gotemplate \
        github.com/micro/protoc-gen-micro \
        && (cd ${GOPATH}/src/github.com/lyft/protoc-gen-validate && make build) \
        && install -c ${GOPATH}/bin/protoc-gen* ${OUTDIR}/usr/bin/

RUN mkdir -p ${GOPATH}/src/github.com/pseudomuto/protoc-gen-doc && \
        curl -L https://github.com/pseudomuto/protoc-gen-doc/archive/v${PROTOC_GEN_DOC_VERSION}.tar.gz | tar xvz --strip 1 -C ${GOPATH}/src/github.com/pseudomuto/protoc-gen-doc
RUN cd ${GOPATH}/src/github.com/pseudomuto/protoc-gen-doc && \
        make build && \
        install -c ${GOPATH}/src/github.com/pseudomuto/protoc-gen-doc/protoc-gen-doc ${OUTDIR}/usr/bin/


FROM ubuntu:16.04 as swift_builder
RUN apt-get update && \
        apt-get install -y build-essential make tar xz-utils bzip2 gzip sed \
        libz-dev unzip patchelf curl libedit-dev python2.7 python2.7-dev libxml2 \
        git libxml2-dev uuid-dev libssl-dev bash patch
ENV SWIFT_VERSION=4.2.1 \
        LLVM_VERSION=5.0.2
RUN curl -L http://releases.llvm.org/${LLVM_VERSION}/clang+llvm-${LLVM_VERSION}-x86_64-linux-gnu-ubuntu-16.04.tar.xz | tar --strip-components 1 -C /usr/local/ -xJv
RUN curl -L https://swift.org/builds/swift-${SWIFT_VERSION}-release/ubuntu1604/swift-${SWIFT_VERSION}-RELEASE/swift-${SWIFT_VERSION}-RELEASE-ubuntu16.04.tar.gz | tar --strip-components 1 -C / -xz

ENV SWIFT_PROTOBUF_VERSION=1.2.0
RUN mkdir -p /swift-protobuf && \
        curl -L https://github.com/apple/swift-protobuf/archive/${SWIFT_PROTOBUF_VERSION}.tar.gz | tar --strip-components 1 -C /swift-protobuf -xz
RUN apt-get install -y libcurl4-openssl-dev
RUN cd /swift-protobuf && \
        swift build -c release
RUN mkdir -p /protoc-gen-swift && \
        cp /swift-protobuf/.build/x86_64-unknown-linux/release/protoc-gen-swift /protoc-gen-swift/
RUN cp /lib64/ld-linux-x86-64.so.2 \
        $(ldd /protoc-gen-swift/protoc-gen-swift | awk '{print $3}' | grep /lib | sort | uniq) \
        /protoc-gen-swift/
RUN find /protoc-gen-swift/ -name 'lib*.so*' -exec patchelf --set-rpath /protoc-gen-swift {} \; && \
        for p in protoc-gen-swift; do \
        patchelf --set-interpreter /protoc-gen-swift/ld-linux-x86-64.so.2 /protoc-gen-swift/${p}; \
        done

FROM ubuntu:16.04 as javalite_builder
RUN apt-get update && \
        apt-get install -y bash patch curl patchelf
ENV PROTOC_GEN_JAVALITE_VERSION=3.0.0
RUN mkdir -p /protoc-gen-javalite && \
        curl -L https://repo1.maven.org/maven2/com/google/protobuf/protoc-gen-javalite/${PROTOC_GEN_JAVALITE_VERSION}/protoc-gen-javalite-${PROTOC_GEN_JAVALITE_VERSION}-linux-x86_64.exe > /protoc-gen-javalite/protoc-gen-javalite && \
        chmod 755 /protoc-gen-javalite/protoc-gen-javalite
RUN cp /lib64/ld-linux-x86-64.so.2 \
        $(ldd /protoc-gen-javalite/protoc-gen-javalite | awk '{print $3}' | grep /lib | sort | uniq) \
        /protoc-gen-javalite/
RUN find /protoc-gen-javalite/ -name 'lib*.so*' -exec patchelf --set-rpath /protoc-gen-javalite {} \; && \
        for p in protoc-gen-javalite; do \
        patchelf --set-interpreter /protoc-gen-javalite/ld-linux-x86-64.so.2 --set-rpath /protoc-gen-javalite /protoc-gen-javalite/${p}; \
        done


FROM rust:1.22.1 as rust_builder
ENV RUST_PROTOBUF_VERSION=1.4.3 \
        OUTDIR=/out
RUN mkdir -p ${OUTDIR}
RUN apt-get update && \
        apt-get install -y musl-tools
RUN rustup target add x86_64-unknown-linux-musl
RUN mkdir -p /rust-protobuf && \
        curl -L https://github.com/stepancheg/rust-protobuf/archive/v${RUST_PROTOBUF_VERSION}.tar.gz | tar xvz --strip 1 -C /rust-protobuf
RUN cd /rust-protobuf/protobuf && \
        RUSTFLAGS='-C linker=musl-gcc' cargo build --target=x86_64-unknown-linux-musl --release
RUN mkdir -p ${OUTDIR}/usr/bin && \
        strip /rust-protobuf/target/x86_64-unknown-linux-musl/release/protoc-gen-rust && \
        install -c /rust-protobuf/target/x86_64-unknown-linux-musl/release/protoc-gen-rust ${OUTDIR}/usr/bin/


FROM znly/upx as packer
COPY --from=protoc_builder /out/ /out/
RUN upx --lzma \
        /out/usr/bin/protoc \
        /out/usr/bin/grpc_* \
        /out/usr/bin/protoc-gen-*

FROM debian:stretch
ARG CLOUD_SDK_VERSION=237.0.0
ENV CLOUD_SDK_VERSION=$CLOUD_SDK_VERSION

COPY --from=static-docker-source /usr/local/bin/docker /usr/local/bin/docker
RUN apt-get -qqy update && apt-get install -qqy \
        curl \
        gcc \
        python-dev \
        python-setuptools \
        apt-transport-https \
        lsb-release \
        openssh-client \
        git \
        gnupg \
    && easy_install -U pip && \
    pip install -U crcmod   && \
    export CLOUD_SDK_REPO="cloud-sdk-$(lsb_release -c -s)" && \
    echo "deb https://packages.cloud.google.com/apt $CLOUD_SDK_REPO main" > /etc/apt/sources.list.d/google-cloud-sdk.list && \
    curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add - && \
    apt-get update && \
    apt-get install -y google-cloud-sdk=${CLOUD_SDK_VERSION}-0 \
        google-cloud-sdk-app-engine-python=${CLOUD_SDK_VERSION}-0 \
        google-cloud-sdk-app-engine-python-extras=${CLOUD_SDK_VERSION}-0 \
        google-cloud-sdk-app-engine-java=${CLOUD_SDK_VERSION}-0 \
        google-cloud-sdk-app-engine-go=${CLOUD_SDK_VERSION}-0 \
        google-cloud-sdk-datalab=${CLOUD_SDK_VERSION}-0 \
        google-cloud-sdk-datastore-emulator=${CLOUD_SDK_VERSION}-0 \
        google-cloud-sdk-pubsub-emulator=${CLOUD_SDK_VERSION}-0 \
        google-cloud-sdk-bigtable-emulator=${CLOUD_SDK_VERSION}-0 \
        google-cloud-sdk-cbt=${CLOUD_SDK_VERSION}-0 \
        kubectl && \
    gcloud config set core/disable_usage_reporting true && \
    gcloud config set component_manager/disable_update_check true && \
    gcloud config set metrics/environment github_docker_image && \
    gcloud --version && \
    docker --version && kubectl version --client
VOLUME ["/root/.config"]

COPY --from=packer /out/ /
COPY --from=rust_builder /out/ /
COPY --from=swift_builder /protoc-gen-swift /protoc-gen-swift
RUN for p in protoc-gen-swift protoc-gen-swiftgrpc; do \
        ln -s /protoc-gen-swift/${p} /usr/bin/${p}; \
        done
COPY --from=javalite_builder /protoc-gen-javalite /protoc-gen-javalite
RUN ln -s /protoc-gen-javalite/protoc-gen-javalite /usr/bin/protoc-gen-javalite

RUN apt-get install -y curl && \
        mkdir -p /protobuf/google/protobuf && \
        for f in any duration descriptor empty struct timestamp wrappers; do \
        curl -L -o /protobuf/google/protobuf/${f}.proto https://raw.githubusercontent.com/google/protobuf/master/src/google/protobuf/${f}.proto; \
        done && \
        mkdir -p /protobuf/google/api && \
        for f in annotations http; do \
        curl -L -o /protobuf/google/api/${f}.proto https://raw.githubusercontent.com/grpc-ecosystem/grpc-gateway/master/third_party/googleapis/google/api/${f}.proto; \
        done && \
        mkdir -p /protobuf/github.com/gogo/protobuf/gogoproto && \
        curl -L -o /protobuf/github.com/gogo/protobuf/gogoproto/gogo.proto https://raw.githubusercontent.com/gogo/protobuf/master/gogoproto/gogo.proto && \
        mkdir -p /protobuf/github.com/mwitkow/go-proto-validators && \
        curl -L -o /protobuf/github.com/mwitkow/go-proto-validators/validator.proto https://raw.githubusercontent.com/mwitkow/go-proto-validators/master/validator.proto && \
        mkdir -p /protobuf/github.com/lyft/protoc-gen-validate/gogoproto && \
        mkdir -p /protobuf/github.com/lyft/protoc-gen-validate/validate && \
        curl -L -o /protobuf/github.com/lyft/protoc-gen-validate/gogoproto/gogo.proto https://raw.githubusercontent.com/lyft/protoc-gen-validate/master/gogoproto/gogo.proto && \
        curl -L -o /protobuf/github.com/lyft/protoc-gen-validate/validate/validate.proto https://raw.githubusercontent.com/lyft/protoc-gen-validate/master/validate/validate.proto && \
        chmod a+x /usr/bin/protoc
