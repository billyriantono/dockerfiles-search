FROM gcr.io/cloud-solutions-images/jenkins-k8s-slave

RUN apt-get update
RUN apt-get install -y gcc python-dev python-setuptools python-pip

RUN pip install --no-cache-dir -U crcmod
