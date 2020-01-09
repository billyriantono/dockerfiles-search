FROM nginx:alpine

ARG GIT_COMMIT=unspecified
LABEL git_commit=$GIT_COMMIT

RUN pwd
ENV FORTITUDE=welcome
COPY ./data /usr/share/nginx/html
