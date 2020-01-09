FROM node:lts-slim
WORKDIR /root

RUN apt-get update && apt-get install -y git 
RUN git clone https://github.com/jclulow/vtmc.git 
RUN cd vtmc && npm install

COPY entry.sh /root/
COPY template/* /root/template/

WORKDIR /mnt
RUN chmod -R 777 /root

#ENTRYPOINT ["node","/root/vtmc/cmd/vtmc.js"]
#CMD ["show"]
ENTRYPOINT ["/root/entry.sh"]
