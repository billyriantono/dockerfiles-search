FROM dockertaiga/front
ENV GITLAB_AUTH_VERSION=3.1.1
ENV SLACK_VERSION=3.1
RUN apk --no-cache add subversion
RUN mkdir -p plugins && \
  cd plugins && \
  svn export "https://github.com/taigaio/taiga-contrib-gitlab-auth/tags/$GITLAB_AUTH_VERSION/front/dist"  "gitlab-auth" &&\
  svn export "https://github.com/taigaio/taiga-contrib-slack/tags/$SLACK_VERSION/front/dist" "slack"
RUN apk del subversion
