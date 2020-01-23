FROM ubuntu as shellchecker
RUN apt-get update && apt-get install -y wget xz-utils
RUN mkdir /downloads
RUN wget -O /downloads/shellcheck.tar.xz https://storage.googleapis.com/shellcheck/shellcheck-stable.linux.x86_64.tar.xz
RUN tar -xvf /downloads/shellcheck.tar.xz
RUN chmod +x /shellcheck-stable/shellcheck

FROM alpine
RUN apk add --no-cache py-pip alpine-sdk groff jq less curl bash python nodejs npm
RUN pip install awscli yamllint
ENV SHFMT_VERSION=2.6.4
ADD https://github.com/mvdan/sh/releases/download/v"$SHFMT_VERSION"/shfmt_v"$SHFMT_VERSION"_linux_amd64 /usr/local/bin/shfmt
RUN chmod +x /usr/local/bin/shfmt
COPY --from=shellchecker /shellcheck-stable/shellcheck /usr/local/bin/shellcheck

