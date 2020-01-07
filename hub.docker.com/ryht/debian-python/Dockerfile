FROM ryht/debian:latest
RUN apt-get update && apt-get upgrade -y && \
 apt-get install -y \
  git-core \
  python python-dev libpq-dev python-setuptools && \
 apt-get autoremove -y && \
 apt-get clean
RUN easy_install pip && \
  pip install virtualenv
CMD ["/bin/bash"]
