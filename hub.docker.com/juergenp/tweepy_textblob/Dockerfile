#
# Tweety - textblob image
#

# Pull base image.
FROM python:3

MAINTAINER Juergen Pecher <juergen.pecher@mydropteam.com>

WORKDIR /usr/src/app

COPY requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt

RUN python -m textblob.download_corpora

COPY config.py ./config.py
COPY sentiment.py ./sentiment.py
CMD [ "python", "./sentiment.py" ]
