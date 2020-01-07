FROM alpine:3.10.1

COPY --from=hashicorp/packer:1.4.2 /bin/packer /bin/packer


RUN apk add --no-cache --update \
    ca-certificates \
    ansible \
    openssh

RUN pip3 install --upgrade pip==8.1.1

RUN pip install awscli --upgrade

ENTRYPOINT ["bin/packer"]
