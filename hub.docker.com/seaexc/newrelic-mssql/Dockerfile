FROM mono:latest

# Create app directory
RUN mkdir -p /usr/apps/plugin

ARG GIT_COMMIT
ENV GIT_COMMIT ${GIT_COMMIT}

ARG CI_BUILD
ENV CI_BUILD ${CI_BUILD}

ARG DEPLOY_DATE
ENV DEPLOY_DATE ${DEPLOY_DATE}

# Copy plugin code
COPY ./plugin /usr/apps/plugin/
WORKDIR /usr/apps/plugin/

CMD ["mono", "plugin.exe"]
