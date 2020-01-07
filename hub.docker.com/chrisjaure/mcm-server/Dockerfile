FROM node:8-alpine

COPY . /mcm-server
WORKDIR /mcm-server

RUN ["npm", "install", "--production"]
RUN ["npm", "run", "build"]

EXPOSE 8000

CMD ["npm", "start", "8000"]
