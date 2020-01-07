FROM jmikucki/debian-base

RUN apt-get update -q \
    && DEBIAN_FRONTEND=noninteractive apt-get install -yq --no-install-recommends \
    apt-utils curl openssh-server ca-certificates postfix wget

RUN wget https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh
RUN bash script.deb.sh
RUN apt-get install gitlab-ce
RUN gitlab-ctl reconfigure

CMD ["/bin/bash"]
