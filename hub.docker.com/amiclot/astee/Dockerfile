FROM python:3.7.3
# MAINTAINER Nick Janetakis <nick.janetakis@gmail.com>

RUN apt-get update && apt-get install -qq -y \
  build-essential libpq-dev --no-install-recommends

ENV INSTALL_PATH /snakeeyes

RUN mkdir -p $INSTALL_PATH
ADD requirements.txt $INSTALL_PATH
WORKDIR $INSTALL_PATH
RUN pip3 install -r requirements.txt

ADD . $INSTALL_PATH

# For some reason we can't use the cli package with the --editable flag
RUN pip3 install .

CMD gunicorn -c "config/gunicorn.py" "snakeeyes.app:create_app()"
