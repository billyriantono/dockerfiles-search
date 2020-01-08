FROM google/cloud-sdk:alpine

RUN gcloud components update
RUN gcloud components install kubectl
RUN apk update && apk --no-cache add curl docker py-pip jq && pip install --upgrade pip
RUN pip install yq 
