ARG BASE_TAG
FROM fabon/alpine-review:${BASE_TAG}

RUN apk --no-cache add nodejs npm git && \
    tlmgr install tcolorbox environ trimspaces upquote
