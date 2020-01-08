FROM node:alpine

EXPOSE 4200

RUN npm install -g @angular/cli && \
    ng new my-app --defaults && \
    cd my-app

WORKDIR my-app

CMD ng serve --host 0.0.0.0