FROM gitlab/gitlab-runner:alpine-v10.4.0

COPY entrypoint.sh /usr/local/bin/entrypoint

ENTRYPOINT ["/usr/bin/dumb-init", "/usr/local/bin/entrypoint"]
CMD ["run"]
