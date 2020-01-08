FROM ruby:2.6.3-stretch AS ruby-2.6.3
COPY . .
FROM postgres:10.10 AS postgres-10.10
COPY --from=0 . .
CMD ["postgres","--fsync=off","--full_page_writes=off","--shared_buffers=1024MB","--work_mem=256MB"]