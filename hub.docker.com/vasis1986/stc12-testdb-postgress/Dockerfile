FROM postgres:9.6

COPY mi.sql /docker-entrypoint-initdb.d/

EXPOSE 5432

# Define environment variable
ENV POSTGRES_USER docker
ENV POSTGRES_PASSWORD docker
ENV POSTGRES_DB students
