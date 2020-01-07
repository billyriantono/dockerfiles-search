FROM alpine:3.6

RUN apk update && apk upgrade &&  apk add --no-cache bash git

ENV IMAGE_HOME /var/image_home
VOLUME $IMAGE_HOME

ENTRYPOINT ["sh", "-c", "cd $IMAGE_HOME; $IMAGE_HOME/bootstrap.sh"]