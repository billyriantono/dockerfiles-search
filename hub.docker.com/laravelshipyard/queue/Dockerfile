FROM laravelshipyard/app:latest

# Let's get S6 to supervise our worker process
RUN apk add --no-cache gnupg bash curl git tzdata \
    && wget -O - "https://keybase.io/justcontainers/key.asc" | gpg --import \
    && wget -O - "https://api.github.com/repos/just-containers/s6-overlay/releases/latest" | \
        egrep "browser_download_url.+amd64.+tar.gz" | cut -d : -f 2,3 | tr -d '"' | xargs wget \
    && gpg --verify s6-overlay-amd64.tar.gz.sig s6-overlay-amd64.tar.gz \
    && tar -xvzf s6-overlay-amd64.tar.gz -C / \
    && rm s6-overlay-amd64.tar.gz s6-overlay-amd64.tar.gz.sig \
    && apk del --no-cache gnupg

ENV QUEUE_ARGUMENTS=''

# Put the data for the queue
RUN mkdir /data && chown www-data:www-data /data

ENTRYPOINT [ "/init" ]
