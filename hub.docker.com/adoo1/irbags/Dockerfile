FROM node:carbon

# WORKDIR /usr/src/app

COPY . .

RUN npm i
RUN npm rebuild node-sass
RUN npm run build

# FROM nginx:alpine
# # COPY nginx.conf /etc/nginx/nginx.conf
# COPY --from=build /usr/src/app/dist /usr/share/nginx/html
