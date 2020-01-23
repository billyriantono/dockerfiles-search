############################################################## FROM VARIABLE ###
ARG os_version=bionic


################################################################ BUILD STAGE ###
FROM ubuntu:${os_version}


################################################################# MAINTAINER ###
MAINTAINER Mijail Molina Lavrishcheva <mijail@edutin.com>
LABEL maintainer="Mijail Molina Lavrishcheva <mijail@edutin.com>"
LABEL "com.edutin"="Edutin Inc."


################################################################ DESCRIPTION ###
LABEL version="1.1"
LABEL description=" Docker image with a set of tools to create and maintain \
a EKS Kubernetes cluster."


############################################################ BUILD VARIABLES ###
ARG CONFIGS_DIR=${HOME}/.edutin/configs
ARG PYTHON_REQ_FILE=${CONFIGS_DIR}/python-requeriments.txt

### aws-iam-authenticator
ARG AWS_IAM_AUTH_VERSION=1.12.7/2019-03-27
ARG AWS_IAM_AUTH_URL="https://amazon-eks.s3-us-west-2.amazonaws.com/\
${AWS_IAM_AUTH_VERSION}/bin/linux/amd64/aws-iam-authenticator"

### eksctl
ARG EKSCTL_VERSION=latest_release
ARG EKSCTL_URL="https://github.com/weaveworks/eksctl/releases/download/\
${EKSCTL_VERSION}/eksctl_linux_amd64.tar.gz"

### kubectl
ARG KUBECTL_VERSION=1.12.7/2019-03-27
ARG KUBECTL_URL="https://amazon-eks.s3-us-west-2.amazonaws.com/\
${KUBECTL_VERSION}/bin/linux/amd64/kubectl"


###################################################### ENVIRONMENT VARIABLES ###
ENV DEBIAN_FRONTEND noninteractive


########################################################## IMAGE BUILD STEPS ###

### copy requeriment files
ADD files/python-requeriments.txt ${CONFIGS_DIR}/

### update local repositories
RUN apt-get update

### install needed packages
RUN apt-get install -y --no-install-recommends \
                       python3 \
                       python3-distutils \
                       ca-certificates \
                       openssh-client \
                       curl \
                       nano \
                       groff \
                       less \
                       unzip \
                       make \
                       git \
                       gpg \
                       jq \
                       bash-completion

### set python3 as default python version
RUN ln -s /usr/bin/python3 /usr/bin/python

### install pip
RUN curl https://bootstrap.pypa.io/get-pip.py --output - | python

### install requeriments
RUN pip install --no-cache-dir --upgrade -r ${PYTHON_REQ_FILE}

### clean apt cache
RUN apt-get clean && \
    rm -rf /var/lib/lists/* && \
    rm -rf /var/log/apt/*

# ### create a new user called 'ubuntu'
# RUN adduser --disabled-password --gecos '' ubuntu
# RUN adduser ubuntu sudo
# RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers
#
# ### switching to 'ubuntu' user
# USER ubuntu
# WORKDIR /home/ubuntu

### create binaries directory and include in PATH environment variable
RUN mkdir -p ${HOME}/bin && \
    echo 'export PATH=${HOME}/bin:${PATH}' >> ${HOME}/.bashrc

### copy update-kubeconfig script to bin dir
ADD files/update-kubeconfig /root/bin/

### customize nano editor
RUN echo '\n\
set fill -4 \n\
set linenumbers \n\
set mouse \n\
set nonewlines \n\
set smooth \n\
set tabstospaces \n\
set titlecolor black,blue \n\
set statuscolor black,blue \n\
set selectedcolor black,yellow \n\
set numbercolor brightyellow \n\
set keycolor cyan \n\
set functioncolor blue' \
>> /etc/nanorc

### customize bash prompt
RUN echo 'PS1="${debian_chroot:+($debian_chroot)}\[\033[01;34m\]\u@\h:\
\[\033[00m\]\W\[\033[01;34m\]\\\\\$ \[\033[00m\]"' \
>> ${HOME}/.bashrc

### get kubectl
RUN curl -o kubectl -L ${KUBECTL_URL} && \
    chmod +x kubectl && \
    mv kubectl ${HOME}/bin/

### get aws-iam-authenticator
RUN curl -o aws-iam-authenticator -L ${AWS_IAM_AUTH_URL} && \
    chmod +x aws-iam-authenticator && \
    mv aws-iam-authenticator ${HOME}/bin/

### get eksctl
RUN curl -L ${EKSCTL_URL} | tar xz -C ${HOME}/bin

### get helm
RUN curl -L https://git.io/get_helm.sh | bash

### bash force colors
RUN sed -i "s/^#force_color/force_color/g" ${HOME}/.bashrc

### source bash completion
RUN echo '\n\
source /etc/bash_completion \n\
source <(kubectl completion bash) \n\
source <(eksctl completion bash) \n\
source <(helm completion bash) \n\
complete -C "/usr/local/bin/aws_completer" aws' \
 >> ${HOME}/.bashrc

############################################################## EXPOSED PORTS ###
EXPOSE 8080


########################################################## WORKING DIRECTORY ###
WORKDIR /root


################################################################# ENTRYPOINT ###
CMD [ "/bin/bash" ]
