FROM pentacent/alpine-erlang-base:21

LABEL maintainer="Mark Sargento <marksargento.00@gmail.com>"

# Important!  Update this no-op ENV variable when this Dockerfile
# is updated with the current date. It will force refresh of all
# of the base images and things like `apt-get update` won't be using
# old cached versions when the Dockerfile is built.
ENV REFRESHED_AT=2019-02-11

RUN apk add git openssh bash gmp libstdc++

CMD ["/bin/sh"]
