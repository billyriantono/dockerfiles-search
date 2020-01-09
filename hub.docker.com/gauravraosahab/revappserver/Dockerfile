### only for generating docker image for PROD locally ###

FROM nginx:1.13.6

## Copy our default nginx config
COPY nginx/default.conf /etc/nginx/conf.d/
COPY nginx/mime.types /etc/nginx/

## Remove default nginx website
RUN rm -rf /usr/share/nginx/html/*

## Expose port 80
EXPOSE 80

## From 'builder' stage copy over the artifacts in dist folder to default nginx public folder
COPY . /usr/share/nginx/html

CMD ["nginx", "-g", "daemon off;"]