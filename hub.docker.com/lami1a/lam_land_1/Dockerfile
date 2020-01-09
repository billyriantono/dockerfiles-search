FROM node

RUN apt update &&   apt install -y curl 
RUN mkdir -p /var/www/lam_land
WORKDIR /var/www/lam_land

COPY . /var/www/lam_land
RUN npm install

EXPOSE 2222

CMD ["npm", "start"]
