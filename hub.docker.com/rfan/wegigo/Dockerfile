# build stage
FROM golang:1.8 AS build-env
ADD . /go/src/github.com/rfancn/wegigo
RUN cd /go/src/github.com/rfancn/wegigo && make

# final stage
FROM rfan/public:alpine-ansible
ARG   CACHEBUST=1
RUN   mkdir /app && cd /app && \
      wget -q https://github.com/rfancn/ansible-libs/archive/master.zip && \
      unzip master.zip "ansible-libs-master/ansible.cfg" && \
      unzip master.zip "ansible-libs-master/roles/ensure_kubernetes/*" && \
      unzip master.zip "ansible-libs-master/roles/configure_kubernetes/*" && \
      unzip master.zip "ansible-libs-master/roles/kube_rabbitmq/*" && \
      mv ansible-libs-master/* /app && \
      rm -fr ansible-libs-master master.zip
WORKDIR /app
ENV PATH /app:$PATH
COPY --from=build-env /go/src/github.com/rfancn/wegigo/wegigo /app/
ENTRYPOINT ["wegigo", "deploy", "-b", "0.0.0.0"]

