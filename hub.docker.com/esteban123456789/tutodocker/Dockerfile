# Dockerfile lolcat
# for test running : docker run -i esteban123456789/tutodocker  - < Dockerfile
FROM ruby:2.1

LABEL maintainer "<herve leclerc> herve.leclerc@alterway.fr"

ARG version

ENV VERSION ${version:-42.24.0}

RUN mkdir /lolcat

ADD https://github.com/busyloop/lolcat/archive/v$VERSION.tar.gz /

RUN tar xf /v$VERSION.tar.gz -C /lolcat --strip-components=1

WORKDIR /lolcat

RUN gem install lolcat

CMD ["-h"]

ENTRYPOINT ["lolcat","-f"]
