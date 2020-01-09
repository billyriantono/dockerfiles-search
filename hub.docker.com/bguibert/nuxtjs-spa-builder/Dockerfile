FROM node:8

LABEL company="Benjamin Guibert"
LABEL maintainer="contact@bguibert.com"
LABEL version="0.1.0"

WORKDIR /usr/src/app

COPY ./scripts/entrypoint.sh /usr/bin/
RUN chmod +x /usr/bin/entrypoint.sh

# Build the project

ENTRYPOINT [ "/bin/sh", "-ce", "entrypoint.sh 2>&1 | tee /var/build/build.log" ]
