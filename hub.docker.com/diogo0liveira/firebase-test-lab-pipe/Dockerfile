FROM diogo0liveira/google-cloud-sdk:1.0.0
LABEL maintainer="Diogo Oliveira <diogo0liveira@hotmail.com>"

ENV LANG='en_US.UTF-8' \
    LANGUAGE='en_US:en' \
    LC_ALL='en_US.UTF-8'

COPY pipe /
COPY LICENSE.txt pipe.yml README.md /
RUN wget -P / https://bitbucket.org/bitbucketpipelines/bitbucket-pipes-toolkit-bash/raw/0.5.0/common.sh
RUN chmod a+x /pipe.sh

ENTRYPOINT ["/pipe.sh"]
