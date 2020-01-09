FROM    milashenko/node

# Bundle app source
COPY package.json /home/node/package.json
RUN cd /home/node && npm --loglevel info install
COPY . /home/node/
# Install app dependencies
#USER root
#RUN chown -R node:node /home/node 
WORKDIR /home/node/
USER node

EXPOSE  3000
CMD ["npm", "start"]
