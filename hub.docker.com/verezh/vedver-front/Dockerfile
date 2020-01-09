FROM node:10

# Setting working directory. All the path will be relative to WORKDIR
WORKDIR '/app'

# Installing dependencies
COPY package*.json ./
RUN npm install

# Copying source files
COPY . .

# Building app
RUN npm run build

# Running the app
CMD [ "npm", "start" ]

# https://medium.com/@khwsc1/a-simple-react-next-js-app-development-on-docker-6f0bd3f78c2c
# docker build -t verezh/vedver-front:latest .
# docker run -d -p 8081:3000 verezh/vedver-front:latest
# docker push verezh/vedver-front:latest 
# docker image rm --force 