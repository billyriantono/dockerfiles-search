FROM oneapm/docker-oneapm-ci-agent:latest

COPY dummy_support_aliyun_container.sh /dummy_support_aliyun_container.sh
RUN chmod +x /dummy_support_aliyun_container.sh

COPY entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh
