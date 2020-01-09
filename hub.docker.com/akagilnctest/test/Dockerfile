FROM gradle

USER root
ADD ./ .
RUN cd xunyingge-admin \
    && gradle build
RUN sleep 30s \
    && cd xunyingge-app \
    && gradle build


