FROM mysql:5.6

# Copy the OpenMRS database schema to the /data directory
ADD openmrs-platform-database.sql /docker-entrypoint-initdb.d/openmrs-platform-database.sql
