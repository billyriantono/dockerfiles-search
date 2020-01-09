FROM archlinux:latest
MAINTAINER ksh2ksk4 <ksh2ksk4+docker.com@gmail.com>

ENV DISTRIBUTIONS='./distributions' \
    MARIADB_DATADIR='/var/lib/mysql' \
    TIMEZONE='Asia/Tokyo'

WORKDIR /root

# Disk size
#   gcc: 200MB
#   mariadb: 400MB
#   Rust: 1.3GB
RUN ln -sfv /usr/share/zoneinfo/${TIMEZONE} /etc/localtime && \
    pacman -Syu --noconfirm && \
    pacman -S --noconfirm \
      base \
      base-devel \
      fish \
      mariadb \
      mariadb-clients && \
    curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs >rustup-init && \
    chmod 755 rustup-init && \
    ./rustup-init -y && \
    rm -f ./rustup-init && \
    ./.cargo/bin/cargo install fd-find ripgrep && \
    ./.cargo/bin/cargo install diesel_cli --no-default-features --features mysql

COPY ${DISTRIBUTIONS}/entrypoint.sh /root/
COPY ${DISTRIBUTIONS}/configs/fish/config.fish /root/.config/fish/
COPY ${DISTRIBUTIONS}/configs/mariadb/001_setup.sql /root/tmp/
COPY ${DISTRIBUTIONS}/configs/mariadb/maria.cnf /etc/my.cnf.d/

# この実行順序は重要
RUN mysql_install_db --basedir=/usr --datadir=${MARIADB_DATADIR} --user=mysql
VOLUME ${MARIADB_DATADIR}

EXPOSE 3306

ENTRYPOINT ./entrypoint.sh
