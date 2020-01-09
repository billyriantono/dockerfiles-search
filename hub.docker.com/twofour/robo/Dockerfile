FROM twofour/php-cli:latest

ARG ROBO_VERSION=1.3.3
COPY src /
RUN robo-setup
ENTRYPOINT ["robo-entrypoint"]
CMD ["robo"]
