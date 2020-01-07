FROM golang:1.12-alpine

RUN apk -Uuv add ca-certificates git openssh \
    && mkdir -p ~/.ssh && umask 0077 \
    && git config --global url."git@bitbucket.org:".insteadOf https://bitbucket.org/ \
	&& git config --global url."git@github.com:".insteadOf https://github.com/ \
	&& ssh-keyscan bitbucket.org >> ~/.ssh/known_hosts \
	&& ssh-keyscan github.com >> ~/.ssh/known_hosts

ADD script.sh /bin/script.sh
ENTRYPOINT /bin/script.sh
