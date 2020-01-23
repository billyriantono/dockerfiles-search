FROM node:10 as base
RUN mkdir /app
WORKDIR /app
COPY . .
RUN npm install

FROM base as build
ARG REACT_APP_GOOGLE_CLIENT=""
ENV REACT_APP_GOOGLE_CLIENT=$REACT_APP_GOOGLE_CLIENT
ARG REACT_APP_API=""
ENV REACT_APP_API=$REACT_APP_API
RUN npm run build

FROM nginx:1.16-alpine
COPY --from=build /app/build /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]