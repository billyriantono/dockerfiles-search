# docker build -t tmpclips/record:latest .
# docker tag tmpclips/record:latest gcr.io/august-gradient-257616/tmpclips/record:latest
# docker push gcr.io/august-gradient-257616/tmpclips/record:latest

# docker hub
# docker push tmpclips/record:latest
# docker run -dit docker.io/tmpclips/record:latest
# docker exec -it {CONTAINER_ID} /bin/bash

FROM ubuntu:19.04
USER root

RUN apt-get update && apt-get install -y vim tesseract-ocr tesseract-ocr-eng ffmpeg python-pip python3-pip psmisc wget unzip
RUN pip3 install algoliasearch bs4 cloudflare numpy psutil requests requests_cache requests_oauthlib psycopg2-binary google-cloud google-cloud-storage Pillow pytesseract editdistance firebase_admin

# Install eng traineddata and replace existing one.
RUN cd /usr/share/tesseract-ocr/4.00/tessdata && wget https://github.com/tesseract-ocr/tessdata/raw/master/eng.traineddata && mv eng.traineddata.1 eng.traineddata

# Install youtube-upload
RUN pip install --upgrade google-api-python-client oauth2client progressbar2
RUN wget https://github.com/tokland/youtube-upload/archive/master.zip
RUN unzip master.zip
RUN cd youtube-upload-master && python setup.py install

RUN mkdir /root/ftg
RUN mkdir /root/ftg/clips
ADD tasks /root/ftg/tasks

ENV game_id none
WORKDIR /root/ftg/tasks
CMD ["sh", "-c", "python3 start.py ${game_id}"]
