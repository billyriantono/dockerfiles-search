FROM certbot/certbot:latest

MAINTAINER <jpreuss@pavuciny.com>

RUN apk add --no-cache gcc g++ libxml2-dev libxslt-dev && \
    pip install dns-lexicon && \
    pip install dns-lexicon[subreg] && \
    lexicon --version && \
    apk del gcc g++;
