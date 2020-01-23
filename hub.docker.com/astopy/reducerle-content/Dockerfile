FROM python:2.7-alpine as builder
ARG sdk_url="http://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-175.0.0-linux-x86_64.tar.gz"
ARG uid=1000

RUN adduser -D -u $uid -G users user

WORKDIR /home/user
USER user
RUN wget ${sdk_url} -O - | tar xz
	
ENV PATH="$PATH:/home/user/google-cloud-sdk/bin"

RUN gcloud components install alpha
RUN gcloud components install app-engine-python

# workaround for getting a wierd error later when copying
# COPY failed: lstat /var/lib/docker/overlay2/8ef0.../merged/home/user/google-cloud-sdk/.install/.backup/.install/.backup: no such file or directory
RUN tar cvz /home/user | tar xvz -C /tmp/


FROM python:2.7-alpine
ARG uid=1000

RUN apk add --no-cache openssh-client

RUN adduser -D -u $uid -G users user

COPY --from=builder /tmp/home/user/ /home/user/
ENV PATH="$PATH:/home/user/google-cloud-sdk/bin"

WORKDIR /home/user
USER user
