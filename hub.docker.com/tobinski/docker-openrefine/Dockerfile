#
# Dockerfile for openrefine
#

FROM vimagick/openrefine

MAINTAINER tobinski

# remove the hard coded minimum memory footprint
RUN apk update && apk add --no-cache sed && sed -e s/REFINE_MIN_MEMORY=1400M//g -i /app/refine.ini
