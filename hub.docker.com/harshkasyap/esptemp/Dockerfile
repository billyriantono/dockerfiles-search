FROM alpine

MAINTAINER Harsh Kasyap<harshkasyap@gmail.com>

# install dependencies
RUN apk update && apk upgrade
RUN apk add npm 
RUN apk add git 
RUN apk add openssh-client
RUN apk add tzdata

# set your timezone
RUN ln -fs /usr/share/zoneinfo/Asia/Kolkata /etc/localtime
RUN apk del tzdata

RUN git clone --single-branch --branch release-cse@iitp https://github.com/harshkasyap/ESPAutomation.git
RUN ln -fs /NexmoPrivateKey/private.key /ESPAutomation/ServerAutomation/private.key
RUN apk del git
RUN apk del openssh-client 
RUN npm --prefix ESPAutomation/ServerAutomation i ESPAutomation/ServerAutomation
CMD npm --prefix ESPAutomation/ServerAutomation start 5000

EXPOSE 5000

# Help and Instructions

# If you have docker installed, You can run this and have Image Up And Running
# docker run --name esptemp -d -p 5000:5000 -v NexmoPrivateKeyLocation:/NexmoPrivateKey -it harshkasyap/esptemp:cseiitp_v1.0
# Then, Play with below commands
# docker start esptemp and docker stop esptemp
# Ready to run in local Network as ip_address:5000

# Pre-Requisites
# You should have ssh-keygen generated and public key addded with your github account
# keep id_rsa file in current folder having dockerfile
# keep Nexmo private.key file in current folder having dockerfile
# docker build -t <image_name:tag> .
# Run it from where you have kept dockerfile. to build the docker image.
# docker run --name esptemp -d -p 5000:5000 -v NexmoPrivateKeyLocation:/NexmoPrivateKey -it <image_name:tag>
# Ready to run in local Network as ip_address:5000

# Replace NexmoPrivateKeyLocation with The folder having Nexmo private.key
# Change port number if required (at all places in dockerfile)