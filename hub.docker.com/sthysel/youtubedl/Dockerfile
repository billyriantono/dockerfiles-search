FROM python:3.5
MAINTAINER https://github.com/sthysel/docker-youtube-dl

RUN groupadd -g 1000 pirates
RUN useradd --uid 1000 --gid 1000 pirate

VOLUME /download
WORKDIR /download

RUN pip install --upgrade youtube_dl

USER pirate
ENTRYPOINT ["youtube-dl"]
CMD ["--help"]
