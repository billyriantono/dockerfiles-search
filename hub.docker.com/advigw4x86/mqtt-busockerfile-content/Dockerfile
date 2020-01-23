FROM python:3.6 as base

# copy the python requirements file to an intermediate container
COPY requirements.txt .

# installing modules
RUN pip3 install -r requirements.txt

# Installing kubectl package
RUN curl -sLO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl

RUN chmod +x ./kubectl

RUN mv ./kubectl /usr/local/bin/kubectl

RUN curl -O https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-231.0.0-linux-x86_64.tar.gz

FROM google/cloud-sdk as extras
COPY --from=base / .

# extra dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
		jq \
	&& rm -rf /var/lib/apt/lists/*
  
