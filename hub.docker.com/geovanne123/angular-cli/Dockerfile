FROM node:10-alpine as builder

MAINTAINER "geovanne queiroz"

WORKDIR /app

#install git
RUN apk add git

#import projetct
RUN git clone https://github.com/creativetimofficial/light-bootstrap-dashboard-angular2.git

#instlal requirement
RUN cp -R light-bootstrap-dashboard-angular2/* /app
RUN npm install -g @angular/cli
RUN npm install

#start server
#CMD ng serve --host 0.0.0.0

# generate buid
RUN  ng build --prod

# image base
FROM nginx:alpine

#configure nginx
COPY  default /etc/nginx/sites-available/default
COPY --from=builder /app/dist/ /usr/share/nginx/html
CMD ["nginx", "-g", "daemon off;"]

 


