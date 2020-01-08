FROM node:4
RUN npm install express
RUN npm install redis
COPY files/ /files/
COPY webui.js /
CMD ["node", "webui.js"]
EXPOSE 8080
LABEL io.openshift.expose-services "8080:http" io.k8s.display-name="dockercoins WebUI"
