FROM jolexa/vizceral-example

MAINTAINER Travix

ENV TURBINE_ENDPOINT=sample_data.json

CMD sed -i "s#request.get('sample_data.json')#request.get('${TURBINE_ENDPOINT}')#" /usr/src/app/src/components/trafficFlow.jsx \
    && npm run dev

