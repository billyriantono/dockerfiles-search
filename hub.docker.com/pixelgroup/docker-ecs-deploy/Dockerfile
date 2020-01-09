FROM docker:stable
MAINTAINER Poeschl@users.noreply.github.com

ENV ECS_DEPLOY_VERSION '3.6.0'
ENV ECS_DEPLOY_SHA256 'c4b8cc8d6c0091905fc63f0b7a9eff558c8f9ec22626c9db1fda0a55cc27ee71'

RUN apk -Uuv add make groff less python py-pip ca-certificates curl bash jq && \
    pip install awscli && \
    apk --purge -v del py-pip && rm /var/cache/apk/* && \
    curl https://raw.githubusercontent.com/silinternational/ecs-deploy/${ECS_DEPLOY_VERSION}/ecs-deploy -o '/usr/local/bin/ecs-deploy' && \
    echo "${ECS_DEPLOY_SHA256}  /usr/local/bin/ecs-deploy" | sha256sum -c

RUN chmod a+x /usr/local/bin/ecs-deploy && ln -s /usr/local/bin/ecs-deploy
