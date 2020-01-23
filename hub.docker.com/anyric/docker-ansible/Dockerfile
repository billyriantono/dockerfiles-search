FROM ubuntu:trusty
MAINTAINER Anyama Richard

#Prevent dpkg error
ENV TERM=xterm-256color

#Set package mirrors to NZ
RUN sed -i "s/http:\/\/archive./http:\/\/nz.archive./g" /etc/apt/sources.list

# Install ansible
RUN apt-get update -qy && \
    apt-get install -qy software-properties-common && \
    apt-add-repository -y ppa:ansible/ansible && \
    apt-get update -qy && \
    apt-get install -qy ansible

# Copy ansible playbook
COPY ansible /ansible

# Add volume for ansible playbook
VOLUME /ansible
WORKDIR /ansible

# Add entrypoint
ENTRYPOINT ["ansible-playbook"]
CMD ["site.yml"]

