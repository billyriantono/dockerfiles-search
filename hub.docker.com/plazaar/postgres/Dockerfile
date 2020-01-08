FROM postgres:10 AS builder
RUN apt update
RUN apt install --yes python python-setuptools ca-certificates postgresql-server-dev-10 build-essential curl
RUN curl https://sh.rustup.rs -sSf | sh -s -- -y
RUN easy_install pgxnclient
RUN PATH="$HOME/.cargo/bin:$PATH" pgxn install jsoncdc --testing

FROM postgres:10
RUN /bin/mkdir -p '/usr/share/postgresql/10/extension'
RUN /bin/mkdir -p '/usr/share/postgresql/10/extension/sql'
RUN /bin/mkdir -p '/usr/share/postgresql/10/extension/doc'
RUN /bin/mkdir -p '/usr/lib/postgresql/10/lib'
RUN /bin/mkdir -p '/usr/share/doc/postgresql-doc-10/extension'
COPY --from=builder /usr/share/postgresql/10/extension/jsoncdc.control /usr/share/postgresql/10/extension/jsoncdc.control
COPY --from=builder /usr/share/postgresql/10/extension/jsoncdc.sql /usr/share/postgresql/10/extension/jsoncdc.sql
COPY --from=builder /usr/share/postgresql/10/extension/uninstall_jsoncdc.sql /usr/share/postgresql/10/extension/uninstall_jsoncdc.sql
COPY --from=builder /usr/lib/postgresql/10/lib/jsoncdc.so /usr/lib/postgresql/10/lib/jsoncdc.so
COPY --from=builder /usr/share/doc/postgresql-doc-10/extension/jsoncdc.md /usr/share/doc/postgresql-doc-10/extension/jsoncdc.md
COPY ./postgresql.conf /etc/postgresql/postgresql.conf
