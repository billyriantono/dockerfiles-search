FROM redis:5.0.6-alpine
FROM th0liveira/base:3.10.2

# MERGE CONTAINER IMAGES -----------------------------------------------------------

COPY --from=redis:5.0.6-alpine / /
COPY --from=th0liveira/base:3.10.2 / /

# PREPARE CONFIGURATIONS -----------------------------------------------------------

# PREPARE DEPENDENCIES -------------------------------------------------------------

# CONFIGURE IMAGE ------------------------------------------------------------------

# -- Prepare Paths
RUN \
    mkdir -p /mnt/data /var/log/redis && \
    chown user:user /mnt/data /var/log/redis

# -- Copy config
COPY config/redis.conf /etc/redis.conf

# CLEAR IMAGE ----------------------------------------------------------------------

# DEFAULTS -------------------------------------------------------------------------

WORKDIR /mnt

# EXPOSE PORT ----------------------------------------------------------------------

EXPOSE 6379

# PREPARE SUPERVISOR FILE ----------------------------------------------------------

RUN echo -e "[program:redis] \n\
command=redis-server /etc/redis.conf --loglevel verbose \n\
user=user \n\
process_name=%(program_name)s_%(process_num)02d \n\
numprocs=1 \n\
autostart=true \n\
autorestart=false \n\
startsecs=0 \n\
redirect_stderr=true \n\
stdout_logfile=/dev/stdout \n\
stdout_logfile_maxbytes=0 " > /etc/supervisord/redis.conf

# RUN COMMAND ----------------------------------------------------------------------
