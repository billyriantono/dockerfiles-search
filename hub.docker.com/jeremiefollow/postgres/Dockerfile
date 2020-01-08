FROM postgres:12

RUN echo "max_connections = 1000" >> /var/lib/postgresql/data/postgresql.conf
RUN echo "shared_buffers = 128MB" >> /var/lib/postgresql/data/postgresql.conf

