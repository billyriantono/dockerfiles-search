FROM node:8.11.3

RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - \
  && echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list

#Trigger build for chrome 78
RUN apt-get update && \
  apt-get install -yq google-chrome-stable=78.0.3904.108-1

CMD [ "node" ]
