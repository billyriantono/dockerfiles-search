FROM tmaier/docker-compose
ENV SERVICE " "
ENV REGISTRY_URL " "
WORKDIR /src
ADD build-push.sh /ci/
CMD exec /ci/build-push.sh
