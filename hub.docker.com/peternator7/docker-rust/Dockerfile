FROM buildpack-deps:jessie-scm

ENV USER root
ADD rust-wrapper /rust-wrapper
RUN /rust-wrapper
WORKDIR application
CMD ["cargo", "build"]