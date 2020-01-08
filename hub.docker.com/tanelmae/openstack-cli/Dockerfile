FROM debian:buster-slim

RUN apt-get update && apt-get upgrade -y
RUN apt -y install curl bash-completion python-magnumclient \
    python-keystoneclient python-novaclient python-glanceclient \
    python-neutronclient python-cinderclient python-heatclient python-openstackclient \
    && rm -rf /var/lib/apt/lists/*

# Bash completion for openstack commands
RUN openstack complete >> /etc/bash.bashrc

# Install latest kubectl
RUN K_VERSION=$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt) && \
    curl -L https://storage.googleapis.com/kubernetes-release/release/${K_VERSION}/bin/linux/amd64/kubectl -o /bin/kubectl && \
    chmod +x /bin/kubectl

RUN adduser stack --gecos "First Last,RoomNumber,WorkPhone,HomePhone" --disabled-password
USER stack
WORKDIR /home/stack
COPY bashrc .bashrc
COPY bash_profile .bash_profile
COPY bash_aliases .bash_aliases
ENTRYPOINT ["/bin/bash"]
