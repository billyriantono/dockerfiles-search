FROM simplygenius/atmos:v0.9.4

ENV TF_VER=0.11.14
ENV TF_PKG=https://releases.hashicorp.com/terraform/${TF_VER}/terraform_${TF_VER}_linux_amd64.zip

RUN apk add git openssh-client python3 py3-pip jq

RUN pip3 install awscli PyGithub click ipython

RUN curl -sL $TF_PKG > terraform.zip && \
    unzip terraform.zip && \
    mv terraform /usr/local/bin && \
    rm -f terraform.zip

RUN if [ ! -e /usr/bin/pip ]; then ln -s pip3 /usr/bin/pip ; fi && \
    if [[ ! -e /usr/bin/python ]]; then ln -sf /usr/bin/python3 /usr/bin/python; fi

COPY comment_on_commit.py /tools/comment_on_commit
