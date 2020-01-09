#Transformer docker file
FROM nvidia/cuda:9.2-devel-ubuntu18.04
MAINTAINER Beibei Tan <bugtan@vip.qq.com>




RUN apt-get -qq update && apt-get -qq -y install curl bzip2 git openssh-server \
    && curl -sSL https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh -o /tmp/miniconda.sh \
    && bash /tmp/miniconda.sh -bfp /usr/local \
    && rm -rf /tmp/miniconda.sh \
    && conda install -y python=3 \
    && conda update conda \
    && apt-get -qq -y remove curl bzip2 \
    && apt-get -qq -y autoremove \
    && apt-get autoclean \
    && rm -rf /var/lib/apt/lists/* /var/log/dpkg.log \
    && conda clean --all --yes

ENV PATH /opt/conda/bin:$PATH

COPY sshd_config /etc/ssh/
CMD ["/usr/sbin/sshd", "-D"]
RUN echo "root:123" | chpasswd
RUN conda install -y -c derickl torchtext pandas
RUN python -m spacy download en && python -m spacy download fr
RUN conda clean --all --yes
EXPOSE 22
ENTRYPOINT service ssh start && /bin/bash
