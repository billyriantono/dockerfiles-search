FROM python:2.7

MAINTAINER sourceperl <loic.celine@free.fr>

# BUILD_DATE and VCS_REF are immaterial, since this is a 2-stage build, but our build
# hook won't work unless we specify the args
ARG BUILD_DATE
ARG VCS_REF

# Good docker practice, plus we get microbadger badges
LABEL org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.vcs-url="https://github.com/funkypenguin/docker.mqttwarn.git" \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.schema-version="2.2-r1"

# build /opt/mqttwarn
RUN mkdir -p /opt/mqttwarn
RUN mkdir -p /opt/mqttwarn/conf
WORKDIR /opt/mqttwarn/
RUN mkdir -p /opt/mqttwarn/services
COPY services/ /opt/mqttwarn/services/
COPY conf /opt/mqttwarn/conf/
COPY mqttwarn.py /opt/mqttwarn/
COPY requirements.txt /opt/mqttwarn/

# install python library
RUN pip install -r requirements.txt

# add user mqttwarn to image
RUN groupadd -r mqttwarn && useradd -r -g mqttwarn mqttwarn
RUN chown -R mqttwarn /opt/mqttwarn

# process run as mqttwarn user
USER mqttwarn

# conf file from host
VOLUME ["/opt/mqttwarn/conf"]

# set conf path
ENV MQTTWARNINI="/opt/mqttwarn/conf/mqttwarn.ini"

# run process
CMD python mqttwarn.py
