FROM ubuntu AS data

WORKDIR /data/
RUN apt-get update \
 && apt-get install -y wget
RUN wget -cO - http://pjreddie.com/media/files/cifar.tgz |tar xfvz -

FROM qnib/data-container-base
COPY --from=data /data /data
