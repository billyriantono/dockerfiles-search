FROM node:4-onbuild

COPY ./package.json /opt/ashpr/xevil/package.json
WORKDIR /opt/ashpr/xevil/
RUN npm install

WORKDIR /opt/ashpr/xevil/src
ADD 	. /opt/ashpr/xevil/src

EXPOSE 3000

CMD        	["npm", "run-script", "start"]