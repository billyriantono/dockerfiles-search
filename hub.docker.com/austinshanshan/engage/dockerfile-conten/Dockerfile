FROM asterios/mysql

# Replication Slave
RUN echo [mysqld] > /etc/mysql/conf.d/rep-slave.cnf \
	&& echo slave_compressed_protocol	= 1 >> /etc/mysql/conf.d/rep-slave.cnf \
	&& echo sync_master_info		= 0 >> /etc/mysql/conf.d/rep-slave.cnf \
	&& echo sync_relay_log			= 0 >> /etc/mysql/conf.d/rep-slave.cnf \
	&& echo sync_relay_log_info		= 0 >> /etc/mysql/conf.d/rep-slave.cnf \
	&& echo master-retry-count		= 86400 >> /etc/mysql/conf.d/rep-slave.cnf \
	&& echo server-id			= 2 >> /etc/mysql/conf.d/rep-slave.cnf \
	&& echo relay-log			= /var/log/mysql/relay >> /etc/mysql/conf.d/rep-slave.cnf \
	&& echo relay-log-index			= /var/log/mysql/relay.index >> /etc/mysql/conf.d/rep-slave.cnf \
	&& echo relay-log-space-limit		= 96M >> /etc/mysql/conf.d/rep-slave.cnf \
	&& echo max-relay-log-size		= 32M >> /etc/mysql/conf.d/rep-slave.cnf \
	&& echo relay-log-recovery		= 1 >> /etc/mysql/conf.d/rep-slave.cnf

RUN sed -re 's/max_connections = ([0-9]+)/max_connections = 256/g' -i /etc/mysql/conf.d/customs.cnf \
	&& sed -re 's/key_buffer_size = ([0-9]+)M/key_buffer_size = 1M/g' -i /etc/mysql/conf.d/customs.cnf
