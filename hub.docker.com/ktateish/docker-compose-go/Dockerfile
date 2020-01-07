FROM skame/docker-compose

RUN curl -Lo go.tgz https://storage.googleapis.com/golang/go1.8.1.linux-amd64.tar.gz \
	&& tar zxvf go.tgz -C /usr/local \
	&& rm -rf go.tgz \
	&& echo 'PATH=/usr/local/go/bin:$PATH' > /etc/profile.d/go.sh \
	&& source /etc/profile.d/go.sh \
	&& curl -Lo protoc.zip https://github.com/google/protobuf/releases/download/v3.2.0/protoc-3.2.0-linux-x86_64.zip \
	&& unzip -d /usr/local protoc.zip \
	&& rm -f protoc.zip \
	&& go get -u github.com/golang/protobuf/proto github.com/golang/protobuf/protoc-gen-go google.golang.org/grpc \
	&& apk add make
