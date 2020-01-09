FROM node as build
ADD . /frontend/
WORKDIR /frontend
RUN npm install
RUN npm run build

FROM nginx:alpine
COPY --from=build /frontend/dist /usr/share/nginx/html
EXPOSE 80
