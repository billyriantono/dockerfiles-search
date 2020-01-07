# Our custom image for Postgres
FROM postgres:11.2

# Create a dir for our custom configs
RUN su - postgres -c "mkdir -p /var/lib/postgresql/configs"

# Add custom HBA file. Enforce passwords for accessing the database.
ADD --chown=postgres:postgres ./provisioning/configs/pg_hba.conf /var/lib/postgresql/configs/pg_hba.conf

# Add custom config file. Prevent end user from making config changes.
ADD --chown=postgres:postgres ./provisioning/configs/postgresql.conf /var/lib/postgresql/configs/postgresql.conf

# Add custom DB init script
ADD --chown=postgres:postgres ./provisioning/postgresql-initdb/init-db.sql /docker-entrypoint-initdb.d/init-db.sql

# Run with the above configs
CMD ["postgres",  "-c", "hba_file=/var/lib/postgresql/configs/pg_hba.conf", \ 
	"-c", "config_file=/var/lib/postgresql/configs/postgresql.conf" ]
