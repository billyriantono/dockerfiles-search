FROM centos
ENV container docker
RUN (yum check-update || true)
RUN curl -fsSL https://get.docker.com/ | sh
RUN systemctl enable docker.service
CMD ["bash"]
