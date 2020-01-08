FROM synapsetec/nodejs:node7
WORKDIR /opt/workapp
COPY . /opt/workapp 
RUN npm install
EXPOSE 3000
CMD ["pm2-docker", "start", "pm2_dev.yaml"]