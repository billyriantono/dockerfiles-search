FROM node:10-slim
MAINTAINER Kitsu, Inc.

LABEL version="1.1.0"
LABEL repository="http://github.com/1Q1-Open-Source/ember-cli-actions"
LABEL homepage="http://github.com/1Q1-Open-Source/ember-cli-actions"
LABEL maintainer="Samuel Bishop <sam@oneqone.com>"

LABEL com.github.actions.name="GitHub Action for Ember-CLI"
LABEL com.github.actions.description="Wraps Ember-CLI to enable common commands."
LABEL com.github.actions.icon="terminal"
LABEL com.github.actions.color="orange"
COPY LICENSE README.md /

RUN npm install -g ember-cli
COPY "entrypoint.sh" "/entrypoint.sh"
ENTRYPOINT ["/entrypoint.sh"]

CMD ["help"]
