FROM zorbash/kitto

ENV MIX_ENV prod
ENV KITTO_IP 0.0.0.0
ENV KITTO_PORT 4000

RUN mkdir /dashboard
WORKDIR /dashboard

ADD . /dashboard


RUN mix deps.get && npm install --silent

RUN npm run build
RUN mix compile

CMD mix kitto.server
