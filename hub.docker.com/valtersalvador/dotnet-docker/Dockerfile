ARG TAG=2.1.402-sdk
FROM microsoft/dotnet:${TAG} AS watcher

LABEL maintainer="valtersalvador@outsmarting.com.br"

ENV DOTNET_USE_POLLING_FILE_WATCHER 1

ARG SOLUTION_NAME=app
ARG PROJECT_DIR=src
WORKDIR /${SOLUTION_NAME}/${PROJECT_DIR}

EXPOSE 5000-5001

ENTRYPOINT [ "dotnet", "watch", "run", "--urls", "https://0.0.0.0:5000"]
