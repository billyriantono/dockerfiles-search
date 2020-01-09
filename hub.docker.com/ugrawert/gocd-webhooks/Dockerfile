FROM almir/webhook:2.6.10

# ENV SECRET=WEBHOOK_SECRET
# ENV GO_API_TOKEN=GO_ADMIN_USER_TOKEN
# ENV GO_SERVER_URL=http://localhost:8153

RUN apk add --update curl

WORKDIR /opt/webhook
ADD relay.sh .
ADD hooks.json .

CMD ["-template", "-hooks=/opt/webhook/hooks.json"]
