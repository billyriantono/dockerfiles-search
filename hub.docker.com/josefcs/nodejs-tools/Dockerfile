FROM node:6.6

WORKDIR /data
ENV HOME=/data

# install all dependencies needed for angular2
RUN npm install -g grunt-cli typescript rxjs zone.js @angular/cli @angular/compiler-cli @angular/platform-server \
 @angular/animations @angular/core @angular/common @angular/compiler @angular/platform-browser \
 webpack tslint source-map-explorer \
 && npm set cache /data/.npm --global

CMD ["bash"]