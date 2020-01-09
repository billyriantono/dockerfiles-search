FROM centos:latest
MAINTAINER https://blog.51cto.com/andyxu/2299916
ENV TIME_ZOME Asia/Shanghai
ARG go="go"
ARG ng="ngrok"
ADD $go.tar.gz /tmp 
ADD $ng.tar.gz /tmp 
RUN yum -y install gcc gcc-c++ git make \
&& mkdir /data \
&& mv /tmp/$go /data/ \
&& echo 'export PATH=$PATH:/data/go/bin' > /etc/profile.d/go.sh \
&& echo 'export GOROOT="/data/go"' >> /etc/profile.d/go.sh  \
&& source /etc/profile.d/go.sh \
&& mv /tmp/$ng /data \
&& cd /data/$ng \
&& mkdir cert \
&& cd cert \
&& openssl genrsa -out rootCA.key 2048 \
&& openssl req -x509 -new -nodes -key rootCA.key -subj "/CN=my.lyone.top" -days 5000 -out rootCA.pem \
&& openssl genrsa -out device.key 2048 \
&& openssl req -new -key device.key -subj "/CN=my.lyone.top" -out device.csr \
&& openssl x509 -req -in device.csr -CA rootCA.pem -CAkey rootCA.key -CAcreateserial -out device.crt -days 5000 \
&& yes|cp rootCA.pem /data/$ng/assets/client/tls/ngrokroot.crt \
&& yes|cp device.crt /data/$ng/assets/server/tls/snakeoil.crt \
&& yes|cp device.key /data/$ng/assets/server/tls/snakeoil.key \
&& cd /data/$ng/ \
&& GOOS=linux GOARCH=amd64 make release-server \
&& GOOS=linux GOARCH=amd64 make release-client \
&& GOOS=linux GOARCH=arm  make release-client \
&& GOOS=windows GOARCH=amd64 make release-client
WORKDIR /data/ngrok
CMD ["/data/ngrok/bin/ngrokd", "-tlsKey=assets/server/tls/snakeoil.key","-tlsCrt=assets/server/tls/snakeoil.crt","-domain=my.lyone.top"]
