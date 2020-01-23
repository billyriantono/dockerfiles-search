FROM node
RUN mkdir /workspace
ADD server /workspace/server
RUN cd /workspace/server && npm install
WORKDIR /workspace/server
CMD ["npm", "start"]

