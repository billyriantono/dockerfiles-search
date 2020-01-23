FROM centos:7

RUN yum -y update \
    && yum -y install strace net-tools git yum-utils epel-release \
    && yum -y clean all

RUN yum-config-manager -y \
        --add-repo https://mirror.go-repo.io/centos/go-repo.repo \
        --add-repo https://dl.yarnpkg.com/rpm/yarn.repo

RUN curl --silent --location https://rpm.nodesource.com/setup_8.x | bash - \
    && yum -y install nodejs yarn \
    && yarn config set registry 'https://registry.npm.taobao.org'

RUN yum -y install bash git vim wget which htop file bzip2 zeromq zeromq-devel tree openssh-clients golang-1.10.4 postgresql-devel \
    && yum -y clean all \
    && mkdir -p /root/go/{bin,src,pkg}

ENV GOPATH="/root/go" \
    PATH="/root/go/bin:${PATH}"

RUN cd /root \
    && wget -O /root/glide.tgz https://github.com/Masterminds/glide/releases/download/v0.13.2/glide-v0.13.2-linux-amd64.tar.gz \
    && tar xf /root/glide.tgz \
    && mv /root/linux-amd64/glide /root/go/bin/glide \
    && rm -fr /root/glide.tgz /root/linux-amd64 \
    && wget -O /root/go/bin/dep https://github.com/golang/dep/releases/download/v0.5.0/dep-linux-amd64 \
    && wget -O /root/go/bin/mc https://dl.minio.io/client/mc/release/linux-amd64/mc \
    && chmod 755 /root/go/bin/*

RUN curl -qsSL -o conda.sh https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh \
        && bash conda.sh -b -f -u -p /opt/conda \
        && rm -fr conda.sh

ENV PATH="/opt/conda/bin:${PATH}" \
    CONDA_DEFAULT_ENV="base" \
    CONDA_EXE="/opt/conda/bin/conda" \
    CONDA_PREFIX="/opt/conda" \
    CONDA_PYTHON_EXE="/opt/conda/bin/python" \
    CONDA_SHLVL="1"

RUN pip install --upgrade pip
