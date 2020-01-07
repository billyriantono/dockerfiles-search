FROM python:3.8.0

LABEL maintainer "genzouw <genzouw@gmail.com>"

ENV PYTHONSTARTUP="/.startup.py"

RUN pip install \
  sympy \
  matplotlib \
  ;

ADD .startup.py /

ADD ./docker-entrypoint.sh /

ENTRYPOINT ["/docker-entrypoint.sh"]
