FROM gcr.io/google_appengine/nodejs

RUN apt-get update && apt-get install libfontconfig -y 

# installing java
RUN apt-get install -y --no-install-recommends default-jre
RUN apt-get install -y --no-install-recommends default-jdk

COPY package.json /app/
RUN npm install
COPY . /app/
CMD npm start


