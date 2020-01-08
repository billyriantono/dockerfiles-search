FROM library/postgres
ENV POSTGRES_USER postgres
ENV POSTGRES_PASSWORD mypassword
EXPOSE 5432
COPY docker-entrypoint-initdb.d/*.sql /docker-entrypoint-initdb.d/