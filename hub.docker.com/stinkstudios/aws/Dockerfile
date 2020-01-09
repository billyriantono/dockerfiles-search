FROM ubuntu

RUN apt update && apt install -y git-core python-pip python3 jq git-lfs openssh-client
RUN pip install awscli
RUN pip install awsebcli
RUN git lfs install --skip-smudge
