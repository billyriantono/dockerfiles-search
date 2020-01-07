FROM python:3.6

ADD requirements.txt /tmp/image_building/requirements.txt
WORKDIR  /tmp/image_building
RUN python -m pip install -r requirements.txt
RUN python -m nltk.downloader -d /usr/share/nltk_data all
RUN python -m spacy download en

