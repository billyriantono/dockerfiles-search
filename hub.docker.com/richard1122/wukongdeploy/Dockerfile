FROM node:latest
WORKDIR /srv


VOLUME ["/var/log/nginx"]

RUN apt-get update && apt-get -y install nginx

ENV WUKONG_BACKEND_VERSION   591a1c47ee5b484803699c86fd4758dae8323524
ENV WUKONG_FRONTEND_VERSION  fdca184d56cbe38ffc2e6aa70a0461936d742ba2

RUN git clone --bare https://github.com/GyrosWorkshop/Wukong.git Wukong.git
RUN git clone --bare https://github.com/GyrosWorkshop/WukongWeb.git WukongWeb.git

RUN mkdir -p Wukong && cd Wukong \
 && git init --separate-git-dir ../Wukong.git . \
 && git checkout ${WUKONG_BACKEND_VERSION} \
 && npm install && npm run typings && npm run build
RUN mkdir -p WukongWeb && cd WukongWeb \
 && git init --separate-git-dir ../WukongWeb.git . \
 && git checkout ${WUKONG_FRONTEND_VERSION} \
 && npm install && npm run build

COPY nginx.conf /etc/nginx/nginx.conf
COPY nginx.default.conf /etc/nginx/sites-available/default

EXPOSE 80

CMD nginx && cd Wukong && npm run start
