# based on Node.js, to build and compile Angular
FROM node:10-alpine AS webbase

# Linux setup
RUN apk update
RUN apk add --update alpine-sdk
# RUN apk del alpine-sdk
RUN apk add python
RUN apk add openssh
RUN apk add git
RUN rm -rf /tmp/* /var/cache/apk/* *.tar.gz ~/.npm

RUN sed -i -e "s/bin\/ash/bin\/sh/" /etc/passwd

#Angular 8 CLI
RUN npm install -g @angular/cli@8.0.1 --unsafe

WORKDIR /app

ARG SSH_PRIVATE_KEY_PATH
RUN mkdir -p /root/.ssh && \
    chmod 0700 /root/.ssh
COPY /var/HSOffenburg /root/.ssh/id_rsa
RUN chmod 600 /root/.ssh/id_rsa
RUN echo "Host bitbucket.org\n\tStrictHostKeyChecking no\n" >> ~/.ssh/config
RUN cat ~/.ssh/config
# RUN ssh -v git@bitbucket.org
RUN ssh -o StrictHostKeyChecking=no git@bitbucket.org

# Finally, install the app.
ARG APP_VERSION=master
RUN git clone git@bitbucket.org:dmaier95/chatbot-winni.git -b ${APP_VERSION} .
RUN rm -rf node_modules
RUN npm install --no-optional

RUN npm run build:ssr

RUN echo "cd /app && npm run serve:ssr" > /run_app.sh

CMD [ "/bin/sh", "/run_app.sh" ]

FROM webbase as node


FROM nginx:1.13-alpine
COPY --from=node /app/dist/browser/ /usr/share/nginx/html
COPY nginx-custom.conf /etc/nginx/conf.d/default.conf
