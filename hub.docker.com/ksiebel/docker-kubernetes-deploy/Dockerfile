FROM google/cloud-sdk

# install pip
RUN apt-get update && apt-get install -y python-pip

# install requirements
COPY requirements.txt /tmp
RUN pip install --no-cache-dir -r /tmp/requirements.txt

# install helm
RUN curl https://raw.githubusercontent.com/kubernetes/helm/master/scripts/get | bash
