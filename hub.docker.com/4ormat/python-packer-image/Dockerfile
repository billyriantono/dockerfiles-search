FROM hashicorp/packer:1.3.4 AS packer
FROM library/python:3.7.2-alpine3.9

COPY --from=packer /bin/packer /bin/packer
RUN apk add openssh
