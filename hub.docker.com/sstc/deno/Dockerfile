FROM frolvlad/alpine-glibc:alpine-3.10

ENV DENO_VERSION=0.13.0

RUN apk add --no-cache --virtual=.build-deps wget \
    && wget "https://github.com/denoland/deno/releases/download/v$DENO_VERSION/deno_linux_x64.gz" -O deno.gz \
    && gunzip -c deno.gz > /bin/deno \
    && chmod +x /bin/deno \
    && apk del .build-deps \
    && rm deno.gz

CMD ["deno"]
