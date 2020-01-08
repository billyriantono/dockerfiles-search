FROM nicolaka/netshoot:latest
LABEL MAINTAINER="jlandowner"
WORKDIR /app
COPY ./entrypoint.sh .
RUN curl -LO https://dl.k8s.io/v1.16.0/kubernetes-client-linux-amd64.tar.gz
RUN tar xvf kubernetes-client-linux-amd64.tar.gz
RUN cp kubernetes/client/bin/kubectl /usr/local/bin/
RUN chmod +x ./entrypoint.sh
ENTRYPOINT ["./entrypoint.sh"]
