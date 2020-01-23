FROM alpine

RUN apk add --update curl python bash nodejs-npm && npm install npm@5.2.0 -g && npm install jest -g && rm -rf /var/cache/apk/*
ENV HOME /
RUN curl https://sdk.cloud.google.com | bash

ENV PATH /google-cloud-sdk/bin:$PATH

RUN gcloud components install kubectl

COPY google-cloud-auth.sh /google-cloud-auth.sh
RUN chmod u+x /google-cloud-auth.sh

VOLUME ["/.config"]

CMD ["/bin/bash","/google-cloud-auth.sh"]