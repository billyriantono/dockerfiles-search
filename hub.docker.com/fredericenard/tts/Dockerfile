FROM ubuntu:latest
MAINTAINER Frederic Enard "frederic.enard@gmail.com"

RUN apt-get update -y

#Utils

RUN apt-get install -y wget curl unzip

#Python

RUN apt-get install -y python3-pip python3-dev build-essential

#Google chrome 

RUN apt-get install -y libglib2.0-0 libnss3 libgconf-2-4 libfontconfig1 libfontconfig1
RUN wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
RUN apt install -y ./google-chrome-stable_current_amd64.deb
RUN rm google-chrome-stable_current_amd64.deb

#Google cloud SDK

RUN curl https://dl.google.com/dl/cloudsdk/release/google-cloud-sdk.tar.gz > /tmp/google-cloud-sdk.tar.gz
RUN mkdir -p /usr/local/gcloud \
  && tar -C /usr/local/gcloud -xvf /tmp/google-cloud-sdk.tar.gz \
  && /usr/local/gcloud/google-cloud-sdk/install.sh
ENV PATH $PATH:/usr/local/gcloud/google-cloud-sdk/bin

#Source code

COPY . /app
WORKDIR /app

#Chrome driver

RUN wget https://chromedriver.storage.googleapis.com/74.0.3729.6/chromedriver_linux64.zip
RUN rm -f chromedriver
RUN unzip chromedriver_linux64.zip
RUN rm chromedriver_linux64.zip

#Python dependencies

RUN pip3 install -r requirements.txt

#Google cloud authentification

RUN gcloud auth activate-service-account --key-file=tts.json

#MP3 directory

RUN mkdir tmp

#Entrypoint

EXPOSE 5000 2222
ENTRYPOINT ["python3"]
CMD ["app.py"]