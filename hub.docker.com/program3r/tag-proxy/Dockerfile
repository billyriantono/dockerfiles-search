FROM phusion/baseimage

RUN apt-get update -y && apt-get install --no-install-recommends -y -q curl python build-essential git ca-certificates
RUN mkdir /nodejs && curl http://nodejs.org/dist/v7.7.3/node-v7.7.3-linux-x64.tar.gz | tar --absolute-names -xvzf - -C /nodejs --strip-components=1

ENV PATH $PATH:/nodejs/bin
#Install Node
ENV PATH /nodejs/bin:$PATH

#Install Forever
RUN npm install -g forever

#Expose Ports
EXPOSE 443
EXPOSE 80

#Update Packages
RUN apt-get update

#Setup Cert Directory
VOLUME /etc/letsencrypt

#Add Application Code
WORKDIR /root
ADD ./ ./


RUN npm install

#Clean
RUN apt-get clean
RUN apt-get autoremove


ENTRYPOINT ["forever","-v","--sourceDir","/root","--spinSleepTime","3000","--workingDir","/root","main.js"]