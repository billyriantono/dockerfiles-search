FROM alpine

ENV HOME /

ENV PATH /google-cloud-sdk/bin:$PATH

RUN apk add --update curl python bash && rm -rf /var/cache/apk/*

RUN curl https://sdk.cloud.google.com | bash

RUN gcloud components install kubectl gsutil

COPY google-cloud-auth.sh /google-cloud-auth.sh
RUN chmod u+x /google-cloud-auth.sh

VOLUME ["/.config"]

ENTRYPOINT ["/bin/bash","/google-cloud-auth.sh"]