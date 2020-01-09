
FROM node:6.10
MAINTAINER Mario Cho <hephaex@gmail.com>

RUN apt-get update
RUN apt-get install -y git
RUN git clone https://github.com/exsilium/cloud9.git


# Declare volume for workspace storage
RUN mkdir /workspace
WORKDIR /workspace
#VOLUME ["/workspace"]

RUN npm install

# WebUI
EXPOSE 3131
EXPOSE 80
# Debug Port
EXPOSE 15454
# Node listen port
EXPOSE 3000

# Declare environnement variables
ENV C9USER=user
ENV C9PWD=password

# Start container services
#CMD /usr/local/bin/node /c9sdk/server.js --port 80 -w /workspace --listen 0.0.0.0 --auth $C9USER:$C9PWD
CMD ["bin/cloud9.sh", "-w", "/workspace", "-l", "0.0.0.0"]
