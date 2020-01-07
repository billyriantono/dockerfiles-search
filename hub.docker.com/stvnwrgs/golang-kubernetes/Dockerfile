FROM google/golang


RUN apt-get update && apt-get upgrade -y && apt-get install -y \
	wget \
        curl \
        git \
	jq \
	python 

RUN curl https://sdk.cloud.google.com | bash
ENV PATH /root/google-cloud-sdk/bin:$PATH

RUN /root/google-cloud-sdk/bin/gcloud components update kubectl

WORKDIR /go/src/app

CMD ["go-wrapper", "run"]

