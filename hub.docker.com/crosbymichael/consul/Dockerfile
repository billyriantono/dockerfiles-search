FROM ubuntu:18.04 as build

RUN apt-get update && apt-get upgrade -y && apt-get install -y unzip curl

RUN curl -o consul.zip -SsL https://releases.hashicorp.com/consul/1.2.2/consul_1.2.2_linux_amd64.zip
RUN unzip consul.zip

FROM scratch
COPY --from=build /consul /bin/consul
