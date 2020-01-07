FROM postgres:9.5 AS postgres-9.5-for-testing
RUN echo "PostgreSQL 9.5 for CI tests"
CMD ["postgres","--fsync=off","--full_page_writes=off","--shared_buffers=1024MB","--work_mem=256MB"]
    