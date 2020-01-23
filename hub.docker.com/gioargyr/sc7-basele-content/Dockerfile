FROM  ubuntu:latest
LABEL maintainer "https://github.com/gilvancosta/dockerized-ubuntu-lastest-ssh"

# Atualiza o SO
RUN apt-get update
RUN apt-get install -y openssh-server vim curl
RUN mkdir /var/run/sshd

# Configura o SSH
RUN echo 'root:root' |chpasswd
RUN sed -ri 's/^PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config
RUN echo 'Banner /etc/banner' >> /etc/ssh/sshd_config
COPY etc/banner /etc/

# Adiciona o Usuário gilvancosta
RUN useradd -ms /bin/bash gilvancosta
RUN adduser gilvancosta sudo
RUN echo 'gilvancosta:19372846' |chpasswd

# Altera para o usuário gilvancosta
USER gilvancosta

# Instala o NVM e o Node
RUN /bin/bash -l -c "curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.34.0/install.sh | bash"
RUN /bin/bash -l -c ". ~/.nvm/nvm.sh && nvm install node"

# Altera para o usuário root
USER root

# Expôe as portas
EXPOSE 22
EXPOSE 3090

# Cria e configura o ponto de montagem do volume
RUN mkdir /workspace
RUN chmod 777 /workspace
VOLUME /workspace

CMD    ["/usr/sbin/sshd", "-D"]