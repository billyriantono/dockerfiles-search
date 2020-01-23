FROM node:4.6

RUN npm config set unsafe-perm true
RUN apt-get update
RUN apt-get install git
RUN git clone http://git.eclipse.org/gitroot/orion/org.eclipse.orion.client.git
WORKDIR /org.eclipse.orion.client/modules/orionode
RUN npm install --production
RUN npm install pty.js
EXPOSE 8081

CMD ["npm", "start", "orion"]
