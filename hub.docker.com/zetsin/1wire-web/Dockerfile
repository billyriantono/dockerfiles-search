FROM node

# Create app directory
RUN mkdir -p /home/app
WORKDIR /home/app

# Bundle app source
COPY . /home/app
RUN npm install
RUN npm run build

EXPOSE 80
CMD npm start
