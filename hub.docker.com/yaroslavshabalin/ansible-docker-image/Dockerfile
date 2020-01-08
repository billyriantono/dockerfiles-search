FROM blitznote/debootstrap-amd64:17.10

ENV LC_ALL ISO.UTF-8
ENV LANG ISO.UTF-8
ENV LANGUAGE en_US:en
ENV CONDA="/opt/conda"
ENV PATH="$CONDA/bin:$PATH"
RUN curl -kL https://repo.continuum.io/miniconda/Miniconda2-latest-Linux-x86_64.sh -o ~/install.sh && \
    bash ~/install.sh -b -f -p "$CONDA" && \
    rm -f ~/install.sh && \
    conda install -y -c conda-forge netifaces && \
    conda update --yes --all && \
    conda install -y oracle-instantclient && \
    conda clean -ya && \
    rm -rf "$CONDA/pkgs/" && \
    echo "$CONDA/orahome">/etc/ld.so.conf.d/oracle.conf && \
    ldconfig

RUN apt-get -y update && \
    apt-get install -y libaio1 openssh-client rsync && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN pip install --upgrade pip && \
    pip install --no-cache-dir cx_oracle ansible ara pywinrm
RUN mkdir -p /var/log/ansible/hosts && \
    mkdir /etc/ansible && \
    echo -e "[local]\nlocalhost\n" > /etc/ansible/hosts
ENV ANSIBLE_GATHERING smart
ENV ANSIBLE_HOST_KEY_CHECKING False
ENV ANSIBLE_RETRY_FILES_ENABLED False
ENV ANSIBLE_PIPELINING True
WORKDIR /ansible/playbooks

COPY ./docker-entrypoint.sh /usr/local/bin/
RUN TINI_VERSION=`curl https://github.com/krallin/tini/releases/latest | grep -o "/v.*\"" | sed 's:^..\(.*\).$:\1:'` && \
    curl -L https://github.com/krallin/tini/releases/download/v${TINI_VERSION}/tini -o /usr/local/bin/tini && \
    chmod +x /usr/local/bin/tini && \
    chmod +x /usr/local/bin/docker-entrypoint.sh

ENTRYPOINT ["/usr/local/bin/tini", "-g", "--", "/usr/local/bin/docker-entrypoint.sh"]
CMD ["/bin/bash"]
