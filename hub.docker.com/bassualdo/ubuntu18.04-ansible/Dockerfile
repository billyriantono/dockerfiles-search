FROM ubuntu:18.04
LABEL maintainer="Bastian Bukatz"
 
# Install dependencies.
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
       vim \
       apt-utils \
       python-pip \
       python-setuptools \
    && rm -Rf /var/lib/apt/lists/* \
    && rm -Rf /usr/share/doc && rm -Rf /usr/share/man \
    && apt-get clean


# Install Ansible via Pip.
RUN pip install ansible

# Install Ansible inventory file.
RUN mkdir -p /etc/ansible
RUN echo "[local]\nlocalhost ansible_connection=local" > /etc/ansible/hosts

CMD bash
