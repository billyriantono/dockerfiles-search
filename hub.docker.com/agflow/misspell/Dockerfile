FROM alpine:3.9

LABEL maintainer="dev@agflow.com" \
      description="misspell linter based on an alpine image"

RUN wget -O ./install-misspell.sh https://git.io/misspell && \
    sh ./install-misspell.sh -b /usr/local/bin

ENTRYPOINT ["misspell"]
CMD ["-help"]
