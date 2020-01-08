# Dockerfile for Hyperledger Explorer PostgreSQL Docker Image
FROM postgres:10.3
MAINTAINER Xi Ning Wang <osswangxining.github.com>

COPY explorerpg.sql /docker-entrypoint-initdb.d/
COPY my-postgres.conf /etc/postgresql/postgresql.conf
