FROM feddamisch/solus:latest as builder

# Build as the root user.
USER root
WORKDIR /

# Install base system packages.
RUN eopkg update-repo -D /target -y && \
    eopkg install baselayout --ignore-safety -D /target -y && \
    eopkg install python3 --ignore-safety -D /target -y && \
    eopkg install -c system.base perl -D /target -y && \
    eopkg install lsb-release man-db nano -D /target -y

FROM scratch

# Copy files from builder image.
COPY --from=builder /target /

RUN (usysconf run -f || true) && \
    # Delete package cache.
    eopkg delete-cache -y && \
    eopkg clean -y && \
    # Copy base configuration files.
    cp -rfv /usr/share/baselayout/* /etc/ && \
    # Create user "docker".
    useradd -m -s /bin/bash docker && \
    echo "docker:null" | chpasswd -e && \
    echo "docker ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/docker && \
    chown -R docker:docker /home/docker && \
    # Disable root user.
    passwd -d root && \
    # Add a "systemd-journal" group so usysconf works.
    groupadd systemd-journal

# Set user "docker" as default.
USER docker
WORKDIR /home/docker

CMD ["/bin/bash"]
