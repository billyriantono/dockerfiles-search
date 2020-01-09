FROM node:10 AS ui-build
RUN npm install -g @angular/cli
RUN git clone https://github.com/dcsfuerth/docker-workshop-zitate.git
WORKDIR /docker-workshop-zitate/frontend
RUN npm install --silent && ng build --prod

FROM nginx:alpine AS ui-server
COPY --from=ui-build /docker-workshop-zitate/frontend/dist/ZitateApp/ /usr/share/nginx/html
