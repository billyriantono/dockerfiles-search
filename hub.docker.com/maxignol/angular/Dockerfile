FROM node as ngbuild

LABEL MAINTENER="Maxence Lebrun <maxence.lebrun.pro59@gmail.com>"

WORKDIR /home/node/app
#COPY tout les fichiers dans le WORKDIR
COPY . .
RUN npm install \
    && npm run build --prod --output-path=dist

FROM nginx:1.17.0-alpine

COPY --from=ngbuild /home/node/app/dist/AngularDocker /usr/share/nginx/html

CMD [ "nginx", "-g", "daemon off;" ]