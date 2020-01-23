FROM	centos:7
RUN	yum install -y https://centos7.iuscommunity.org/ius-release.rpm && \
	yum install -y python36u python36u-libs python36u-devel python36u-pip \
	unzip gcc
RUN	pip3.6 install \
	pandas matplotlib numpy scikit-learn scipy \
	ipython jupyter jupyterthemes jupyter_contrib_nbextensions jupyter_contrib_nbextensions \
	boto3 botocore awscli
RUN	useradd jupyter
USER	jupyter
RUN	mkdir -p /home/jupyter/.local/share/jupyter/kernels && \
	jupyter contrib nbextension install --user && \
	jupyter nbextensions_configurator enable --user
COPY	start.sh /
ENV	PYTHONIOENCODING=utf8
EXPOSE	8888
WORKDIR	/home/jupyter
ENTRYPOINT ["/bin/bash", "/start.sh"]
