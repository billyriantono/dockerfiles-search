
# Create the image based on the official Node 8.9.0 image from Dockerhub
FROM node:9.2.0 as node

# Change directory so that our commands run inside this new directory
WORKDIR /websm

# Copy dependency definitions
COPY package.json /websm

# Install dependencies using npm

# Get all the code needed to run the app
COPY . /websm

#Build the app

RUN npm install

RUN npm cache clean --force

RUN npm run build

#==================== Setting up stage ==================== 
# Create image based on the official nginx - Alpine image
FROM nginx:latest

COPY ./nginx.conf /etc/nginx/conf.d/default.conf

COPY .htpasswd /etc/nginx/

COPY nginx.crt /etc/ssl/

COPY nginx.key /etc/ssl

COPY --from=node /websm/dist/websm /usr/share/nginx/html

EXPOSE 80
