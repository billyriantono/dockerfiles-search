
FROM rabbitmq:3.7-alpine

RUN rabbitmq-plugins enable --offline rabbitmq_management

# extract "rabbitmqadmin" from inside the "rabbitmq_management-X.Y.Z.ez" plugin zipfile
# see https://github.com/docker-library/rabbitmq/issues/207
RUN set -eux; \
	erl -noinput -eval ' \
		{ ok, AdminBin } = zip:foldl(fun(FileInArchive, GetInfo, GetBin, Acc) -> \
			case Acc of \
				"" -> \
					case lists:suffix("/rabbitmqadmin", FileInArchive) of \
						true -> GetBin(); \
						false -> Acc \
					end; \
				_ -> Acc \
			end \
		end, "", init:get_plain_arguments()), \
		io:format("~s", [ AdminBin ]), \
		init:stop(). \
	' -- /plugins/rabbitmq_management-*.ez > /usr/local/bin/rabbitmqadmin; \
	[ -s /usr/local/bin/rabbitmqadmin ]; \
	chmod +x /usr/local/bin/rabbitmqadmin; \
	apk add --no-cache python; \
	rabbitmqadmin --version

EXPOSE 15671 15672 5673
WORKDIR /var/lib/rabbitmq

# install delayed plusin
RUN wget https://dl.bintray.com/rabbitmq/community-plugins/3.7.x/rabbitmq_delayed_message_exchange/rabbitmq_delayed_message_exchange-20171201-3.7.x.zip -P /opt/rabbitmq/plugins && \
    unzip /opt/rabbitmq/plugins/rabbitmq_delayed_message_exchange-20171201-3.7.x.zip -d /opt/rabbitmq/plugins && \
    rm -rf /opt/rabbitmq/plugins/rabbitmq_delayed_message_exchange-20171201-3.7.x.zip && \ 
    ls -al /opt/rabbitmq/plugins && \
    rabbitmq-plugins list && \
    rabbitmq-plugins enable rabbitmq_mqtt rabbitmq_federation_management rabbitmq_stomp rabbitmq_delayed_message_exchange && \
    rabbitmq-plugins list

# install amqproxy
RUN apk add crystal shards bash libc-dev && \
    git clone https://github.com/cloudamqp/amqproxy /opt/rabbitmq/amqproxy && \
    cd /opt/rabbitmq/amqproxy && \
    shards build --release --production && \
    cp /opt/rabbitmq/amqproxy/bin/amqproxy /usr/bin/ && \
    sed -i '$d' /usr/local/bin/docker-entrypoint.sh && \
    echo 'amqproxy -l 0.0.0.0 -p 5673 amqp://127.0.0.1:5672 > /dev/null 2>&1 &' >> /usr/local/bin/docker-entrypoint.sh && \
    echo 'exec "$@"' >> /usr/local/bin/docker-entrypoint.sh
