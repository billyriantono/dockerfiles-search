# base image
FROM node:10.15.3 as builder

# RUN npm config set registry https://registry.npm.taobao.org

RUN mkdir -p /macker-user-front-end

#指定工作目录
WORKDIR /macker-user-front-end

COPY . .

RUN npm install
# generate build
RUN npm run ng build --prod --output-path=nginx/html


### STAGE 2: Setup ###

# base image
FROM nginx:1.17.6-alpine

## Copy our default nginx config
COPY nginx /usr/share/nginx

## Remove default nginx website
#RUN rm -rf /usr/share/nginx/html/*


## copy artifact build from the 'build environment'
#COPY --from=builder /macker-user-front-end/dist /usr/share/nginx/html


# expose port 80
EXPOSE 80

# run nginx
CMD ["nginx", "-g", "daemon off;"]