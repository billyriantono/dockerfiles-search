FROM gcr.io/google_appengine/nodejs

RUN echo ttf-mscorefonts-installer msttcorefonts/accepted-mscorefonts-eula select true | debconf-set-selections
RUN echo "deb http://ftp.uk.debian.org/debian/ jessie main contrib" >> /etc/apt/sources.list

RUN apt-get update
RUN apt-get install -y libfontconfig  

RUN apt-get install -y --allow-unauthenticated ttf-mscorefonts-installer

RUN apt-get -y --allow-unauthenticated install default-jre
RUN apt-get -y --allow-unauthenticated install default-jdk

#ENV GOOGLE_APPLICATION_CREDENTIALS=/app/config/gcloud_ps.json 

COPY package.json /app/
RUN npm install
COPY . /app/
CMD npm start
