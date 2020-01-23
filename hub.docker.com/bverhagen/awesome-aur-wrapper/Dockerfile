ARG WRAPPER=yay
FROM bverhagen/pacman-aur-wrapper:${WRAPPER}

# Add a user to use in the docker container
RUN groupadd -g 42 awesome && useradd -r -u 42 --create-home -g awesome awesome

# Give user root access via sudo
RUN echo "awesome ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

RUN mkdir --parents /.cache && sudo chown awesome:awesome /.cache/

USER awesome
ENV EDITOR false
