FROM damstra/aws-cli

MAINTAINER James Moey <j.moey@damstratechnology.com>
ADD ./backup.sh /backup.sh

ENV BITBUCKET_USER=
ENV BITBUCKET_PASSWORD=
ENV BITBUCKET_REPO_LIST=
ENV S3_BUCKET=

ENTRYPOINT [ "/backup.sh" ]