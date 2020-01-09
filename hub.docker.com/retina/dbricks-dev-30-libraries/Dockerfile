FROM retina/dbricks-dev-20-r:latest

MAINTAINER "Brad Ito" brad@retina.ai

COPY Pipfile /tmp/Pipfile
COPY Pipfile.lock /tmp/Pipfile.lock
RUN cd /tmp \
  && pipenv install --verbose --system

