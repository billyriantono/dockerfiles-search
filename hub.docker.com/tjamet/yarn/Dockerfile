FROM alpine
RUN apk add --no-cache yarn
ENTRYPOINT ["yarn"]
ENV YARN_CACHE_FOLDER=/home/.yarn-cache
ENV PORT=8080
ENV HOST=0.0.0.0
LABEL io.whalebrew.config.volumes='["~/.home.yarn:/home"]'
LABEL io.whalebrew.config.keep_container_user 'true'
LABEL io.whalebrew.config.ports '["8080:8080"]'
LABEL io.whalebrew.config.environment '["HOST", "PORT"]'

