FROM node:6.10

RUN apt-get update
RUN apt-get install -y git
RUN git clone https://github.com/exsilium/cloud9.git
WORKDIR /cloud9
RUN npm install
VOLUME /workspace
EXPOSE 3131

CMD ["bin/cloud9.sh", "-w", "/workspace", "-l", "0.0.0.0"]
