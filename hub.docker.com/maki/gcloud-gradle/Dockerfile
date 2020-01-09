FROM google/cloud-sdk:275.0.0-alpine

MAINTAINER Vadim Homchik <homchik@gmail.com>

RUN apk --update --no-cache add gradle

RUN gcloud components install app-engine-java --quiet

CMD ["gradle"]
