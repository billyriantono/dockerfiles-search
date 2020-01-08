FROM gesila009/centos-7:latest

LABEL author=madehao@e-chinalife.com

RUN groupadd -g 5000 rabbitmq; \
    useradd -g 5000 -u 5000 -m rabbitmq;

RUN yum install -y epel-release; \
    sed -i "s/#baseurl/baseurl/g" /etc/yum.repos.d/epel.repo; \
    sed -i "s/mirrorlist/#mirrorlist/g" /etc/yum.repos.d/epel.repo; \
    sed -i "s@http://download.fedoraproject.org/pub@https://mirrors.huaweicloud.com@g" /etc/yum.repos.d/epel.repo; \
    yum update -y; \
    yum install -y wget; \
    wget https://packages.erlang-solutions.com/erlang-solutions-1.0-1.noarch.rpm; \
    rpm -Uvh erlang-solutions-1.0-1.noarch.rpm; \
    rm -f erlang-solutions-1.0-1.noarch.rpm; \
    rpm --import https://packages.erlang-solutions.com/rpm/erlang_solutions.asc; \
    yum install -y erlang; \
    curl -sL https://packagecloud.io/install/repositories/rabbitmq/rabbitmq-server/script.rpm.sh | bash; \
    yum install -y rabbitmq-server; \
    yum clean all;

RUN curl -sL \
        "https://github.com/tianon/gosu/releases/download/1.11/gosu-amd64" \
        -o /usr/local/bin/gosu; \
    chmod 4755 /usr/local/bin/gosu;

COPY entrypoint.sh /usr/local/bin/

RUN chmod 755 /usr/local/bin/entrypoint.sh /usr/local/bin/gosu;

ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]
CMD ["rabbitmq-server"]

