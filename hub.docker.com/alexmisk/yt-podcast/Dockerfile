# Environement variables expected:
# for youtube-dl: PLAYLIST
# for SFTP-server: SERVER_USER, SERVER_ADDRESS, SERVER_FOLDER, SERVER_PORT

FROM alpine

WORKDIR /app

ADD update_feed.sh /app

RUN \
    # Install dependencies
    apk update && apk upgrade                                    && \
    apk --no-cache add curl python ffmpeg openssh-client bash util-linux   && \
    # Download and install youtube-dl
    curl -L https://yt-dl.org/downloads/latest/youtube-dl           \
         -o /bin/youtube-dl                                      && \
    chmod a+rx /bin/youtube-dl                                   && \
    chmod a+rx /app/update_feed.sh

CMD ./update_feed.sh