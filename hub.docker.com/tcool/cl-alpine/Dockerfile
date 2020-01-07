FROM frolvlad/alpine-glibc:alpine-3.6

# --- general --- #
ARG work_dir=/tmp/setup
RUN mkdir ${work_dir} && \
    chmod 777 ${work_dir}

# --- Postgres --- #
ENV PGDATA /var/lib/postgresql/data
VOLUME /var/lib/postgresql/data

COPY docker-entrypoint.sh /

# --- ENTRYPOINT ["/docker-entrypoint.sh"] --- #

EXPOSE 5432

# --- CMD ["postgres"] --- #


# --- Roswell --- #
RUN apk add --no-cache git automake autoconf make gcc build-base curl-dev curl glib-dev libressl-dev ncurses-dev sqlite libev-dev su-exec libpq postgresql-client postgresql-dev postgresql-contrib && \
    mkdir /docker-entrypoint-initdb.d && \
    chmod +x docker-entrypoint.sh && \
    cd ${work_dir} && \
    git clone --depth=1 -b release https://github.com/roswell/roswell.git && \
    cd roswell && \
    sh bootstrap && \
    ./configure --disable-manual-install && \
    make && \
    make install && \
    cd .. && \
    rm -rf roswell && \
    ros run -q

# --- Add PATH to roswell/bin --- #
ENV PATH /root/.roswell/bin:${PATH}

# --- Caveman, Lem, Darkmatter --- #
RUN ln -s ${HOME}/.roswell/local-projects work && \
    ros install fukamachi/clack && \
    ros install fukamachi/caveman && \
    ros install cxxxr/lem && \
    ros install tamamu/darkmatter && \
    ros install Shinmera/dissect && \
    ros install fukamachi/qlot && \
    ros install fukamachi/utopian && \
    mv ${HOME}/.roswell/bin/lem ${HOME}/.roswell/bin/lem2 && \
    mv ${HOME}/.roswell/bin/lem-ncurses ${HOME}/.roswell/bin/lem

# --- Open a port for running web applications --- #
EXPOSE 8888
