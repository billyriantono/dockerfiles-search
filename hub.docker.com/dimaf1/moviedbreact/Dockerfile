## Multistage build pattern


# build environment
FROM node:12.2.0-alpine as build
WORKDIR /app
ENV PATH /app/node_modules/.bin:$PATH
COPY package.json /app/package.json
COPY package-lock.json /app/package-lock.json
RUN npm install
COPY . /app
RUN npm run build


# production environment
FROM nginx:1.16.0-alpine
COPY --from=build /app/build /usr/share/nginx/html
RUN rm /etc/nginx/conf.d/default.conf
# add custom nginx config for react router support, gzip turned on and cache-control headers set for static files
COPY nginx.conf /etc/nginx/conf.d
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]


## You can build and tag this image with command `docker build -f Dockerfile-prod -t dimaf1/moviedbreact:latest .`
## Once the build is done you can run the container with command `docker run -it -p 80:80 --rm dimaf1/moviedbreact:latest`. Be sure you haven't listeting 80 port by nginx on the host machine 
## This docker image is pushed to Docker hub https://cloud.docker.com/repository/docker/dimaf1/moviedbreact/general so it can be run immediately without build localy
## Deployed to AWS Elastic Beanstalk http://moviedb.eu-central-1.elasticbeanstalk.com/