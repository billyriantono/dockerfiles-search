FROM nginx:1.15.2-alpine

LABEL author="Fan Lin <linfan0558@gmail.com>"

USER root

ENV HOME=/usr/src/
ENV ANGULAR=${HOME}/prof-rating/
ENV DEPLOY=/usr/share/nginx/html/

ENV BUILD_PACKAGES="git nodejs"

WORKDIR ${HOME}

# Set proxy server
# ENV http_proxy http://156.132.20.149:80
# ENV https_proxy http://156.132.20.149:80

RUN apk update \
    && apk add --no-cache ${BUILD_PACKAGES} \
    # Proxy setting
    # && npm config set strict-ssl false \
    # && npm config set registry "http://registry.npmjs.org/" \
    # && npm config set registry "http://registry.npmjs.org/" \
    # && npm config set proxy http://156.132.20.149:80 \
    # && npm config set https-proxy http://156.132.20.149:80 \
    # && export HTTP_PROXY=http://156.132.20.149:80 \
    # GIT pull
    # && git config --global http.sslVerify false \
    && git clone https://github.com/fanlin8/prof-rating.git

# RUN git -C nextgen/ checkout feature/ATeam

WORKDIR ${ANGULAR}

# Build & Deploy
RUN rm -rf node_modules dist && npm install -g @angular/cli@6.0.3 --unsafe \
    && npm install && npm cache clean --force && rm -rf ~/.npm \
    && ng build --prod && cp -R dist/HU-PROF-RATING-APP/* ${DEPLOY} && rm -rf ${ANGULAR}

CMD ["nginx", "-g", "daemon off;"]