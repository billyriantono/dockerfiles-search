FROM node:10.16-alpine

# Tools required to run
RUN apk add --no-cache curl tini
# datadog apm
RUN npm install --save dd-trace
# Install envconsul
RUN curl https://releases.hashicorp.com/envconsul/0.9.0/envconsul_0.9.0_linux_amd64.tgz -o envconsul.tgz && \
    tar -xvzf envconsul.tgz && \
    rm envconsul.tgz && \
    mv envconsul /usr/bin

# set and expose port for nextjs
ENV PORT 8080
EXPOSE 8080

ENTRYPOINT ["/sbin/tini", "--", "/docker-entrypoint.sh"]
CMD ["start"]
