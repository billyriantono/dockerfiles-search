FROM python:2-slim

ENV TRAC_VERSION=1.2.3

RUN apt-get -qq update \
	&& DEBIAN_FRONTEND=noninteractive apt-get -y -qq install locales subversion gcc git-core \
	&& rm -r /var/lib/apt/lists /var/cache/apt/archives

RUN sed -i -e 's/# de_DE.UTF-8 UTF-8/de_DE.UTF-8 UTF-8/' /etc/locale.gen && \
    locale-gen
ENV LANG de_DE.UTF-8  
ENV LANGUAGE de_DE:de  
ENV LC_ALL de_DE.UTF-8   

RUN easy_install \
  Genshi \
  pytz \
  Babel \
  docutils \
  Pygments \
  psycopg2

RUN easy_install Trac==$TRAC_VERSION

EXPOSE 3000

ENTRYPOINT ["tracd"]
CMD ["-p", "3000", "-e", "/trac"]