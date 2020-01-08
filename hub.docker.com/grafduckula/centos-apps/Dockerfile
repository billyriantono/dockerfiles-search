FROM centos/systemd

# ADD entrypoint bash shell file
ADD entrypoint.sh /usr/bin/entrypoint.sh

# Initialization commands
RUN (yum update -y; \
    # Update System and install essential packs
    yum install -y epel-release initscripts wget curl tar zip unzip passwd openssh-server openssl ;\
    # Configure OpenSSH-Server (Part. 1)
    sed -i 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config; \
    sed -i 's/#UsePAM no/UsePAM no/g' /etc/ssh/sshd_config; \
    sed -i 's/#PermitRootLogin yes/PermitRootLogin yes/' /etc/ssh/sshd_config; \
    # Configure OpenSSH-Server (Part. 2)
    mkdir -p /root/.ssh/; \
    echo "StrictHostKeyChecking=no" > /root/.ssh/config; \
    echo "UserKnownHostsFile=/dev/null" >> /root/.ssh/config; \
    # Configure SSH key
    ssh-keygen -A ;\
    # Configure yum repo
    sed -i 's/enabled=0/enabled=1/' /etc/yum.repos.d/CentOS-Base.repo; \
    # Set the root password
    echo "root:toor" | chpasswd ;\
    # Cleaning up images
    yum clean all ;\
    rm -rf /var/cache/yum )

# Preinstall shadowsocks server
RUN (yum update -y ;\
    yum install -y net-tools ;\
    wget --no-check-certificate -O ss.sh https://bitbucket.org/grafduckula/shadowsocks-ease/raw/master/shadowsocks-ease.sh ;\
    chmod +x ss.sh ;\
    mv ./ss.sh /usr/bin/ss.sh ;\
    ss.sh installonly ;\
    yum clean all ;\
    rm -rf /var/cache/yum )

# Preinstall kcptun
RUN (yum update -y ;\
    wget --no-check-certificate -O kcptun.sh https://bitbucket.org/grafduckula/kcptun-ease/raw/master/kcptun-ease.sh ;\
    chmod +x kcptun.sh ;\
    mv ./kcptun.sh /usr/bin/kcptun.sh ;\
    kcptun.sh installonly ;\
    yum clean all ;\
    rm -rf /var/cache/yum )

# Preinstall web service requirements
RUN (yum update -y ;\
    yum install -y jq nginx shellinabox ;\
    yum clean all ;\
    rm -rf /var/cache/yum )

# Expose ports for services
EXPOSE 22/tcp
EXPOSE 443/tcp
EXPOSE 443/udp
EXPOSE 29900/udp
EXPOSE 80/tcp
EXPOSE 4200/tcp

# What to do when start the docker image
ENTRYPOINT [ "bash", "/usr/bin/entrypoint.sh" ]
