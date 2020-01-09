FROM stormforger/cli AS sf-cli
FROM node

COPY --from=sf-cli /bin/forge /bin/forge
RUN apt-get update && apt-get install gettext-base
