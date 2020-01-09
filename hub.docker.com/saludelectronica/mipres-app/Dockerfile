# # Dockerfile Angular
# FROM node:12.13-alpine as builder
# LABEL authors="Salud electronica"
# # RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add -
# # RUN sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list'
# # RUN apt-get update && apt-get install -yq google-chrome-stable
# WORKDIR /app
# RUN npm install -g @angular/cli
# COPY package.json .
# RUN npm install
# COPY . .
# RUN npm run build
# # EXPOSE 4200
# # CMD ["npm","start"]



# # nginx
# FROM nginx:alpine
# #RUN rm -rf /usr/share/nginx/html/*
# RUN ls
# RUN rm -rf /usr/share/nginx/html/*
# COPY --from=builder /app/nginx.conf /etc/nginx/nginx.conf
# COPY --from=builder /app/dist /usr/share/nginx/html
# EXPOSE 80
# CMD ["nginx", "-g", "daemon off;"]

# Dockerfile Angular
FROM node:12.13 as builder
LABEL authors="Salud electronica"
RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add -
RUN sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list'
RUN apt-get update && apt-get install -yq google-chrome-stable
WORKDIR /app
COPY package.json .
RUN npm install
EXPOSE 4200
COPY . .
CMD ["npm","start"]