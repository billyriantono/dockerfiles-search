FROM centos:7
LABEL maintainer="Tim Dudgeon<tdudgeon@informaticsmatters.com>"

RUN yum -y upgrade && \
    yum -y install epel-release && \
    yum -y install python2-pip openssh-clients

RUN useradd -u 5001 -U -G 0 -m tej
ENV HOME /home/tej

WORKDIR ${HOME}
COPY docker-entrypoint.sh ./
COPY requirements.txt ./
COPY start.sh ./
COPY tej-submit.sh ./
RUN pip install --upgrade pip && \
    pip install -r requirements.txt && \
    chown -R 5001.5005 /home/tej && \
    chmod 755 *.sh

USER 5001

CMD ["/home/tej/docker-entrypoint.sh"]
