FROM ubuntu:latest
ENV NODE_PATH /install/node_modules/
ENV PATH /install/node_modules/.bin:$PATH
ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update 
RUN apt-get install -y 
RUN apt-get install git-all -y
RUN apt-get install curl -y
RUN curl -sL https://deb.nodesource.com/setup_12.x | bash
RUN apt-get install nodejs -y
RUN apt-get install -qqy x11-apps
RUN node -v 
RUN npm -v

RUN npm install -g grunt-cli
#RUN gem install listen sass compass scss_lint --no-document

WORKDIR /srv
VOLUME /srv

ENV LC_ALL=C.UTF-8 \
    LANG=en_US.UTF-8 \
    LANGUAGE=en_US.UTF-8

# Install UI5 tooling
RUN npm install grunt-init
RUN npm install grunt
RUN npm install grunt-eslint
RUN npm install grunt-nwabap-ui5uploader
RUN npm config set @sap:registry "https://npm.sap.com" -g
RUN npm install @sap/grunt-sapui5-bestpractice-build
RUN npm install --global @ui5/cli
RUN npm install --global @ui5/uiveri5

RUN curl -s https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add -
RUN echo 'deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main' | tee /etc/apt/sources.list.d/google-chrome.list
#RUN apt-get update
RUN apt-get install chromium-browser -y

#RUN mkdir /usr/local/lib/node_modules/@ui5/uiveri5/selenium
#RUN chmod -R 777 /usr/local/lib/node_modules/@ui5/uiveri5/selenium


# docker-entrypoint
#COPY entrypoint.sh /entrypoint.sh
#ENTRYPOINT ["/entrypoint.sh"]

#CMD ["grunt"]

