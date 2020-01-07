# ------------------------------------------------------
#                       Dockerfile
# ------------------------------------------------------
# image:    youtube-upload-docker
# name:     cic1988/youtube-upload-docker
# authors:  gaoyuanhot@gmail.com
# ------------------------------------------------------

FROM python:3.7.4-alpine3.10

WORKDIR /tmp/youtube-upload

# install dependencies
RUN pip3 install --upgrade google-api-python-client oauth2client progressbar2

# install youtube-upload: https://github.com/tokland/youtube-upload
RUN wget https://github.com/cic1988/youtube-upload/archive/master.zip && \
  unzip master.zip && \
  cd youtube-upload-master && \
  python3 setup.py install

ENTRYPOINT ["youtube-upload"]
