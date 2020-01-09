FROM ubuntu:latest

RUN apt-get update && apt-get install -y openssh-server

ADD bootstrap.sh /

RUN mkdir /var/run/sshd \
  && mkdir /root/.ssh \
  && chmod 700 /root/.ssh \
  && touch /root/.ssh/authorized_keys \
  && chmod 600 /root/.ssh/authorized_keys \
  && chmod 755 /bootstrap.sh
  
ENV SSH_PUBKEY ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEAqpCXSYuxrVK0Ywyh+0a1iemc/cMTG25p+Dzp3Le5KHQewXLJDU3epq5AkexZYuMAs+GenA1v4ZMa5Vt5NVFxlM7paWdK2VwFMkzHVR5jpqSbgO5LlAsB8uz96juT8vJr7Pfu22xDVcitz79aAFksnCOV6x+7e18X8tVPA/j0pqvY8W/j2dNMyai13byZwepqNGn3gFxhSLk37N7XinMR8D6JlliedQV004rm57uoqtaxkrlRCln3EP09lYxFVay/PQ34oplMd9F1UoLD9ontpcO1apcE5YzraQhTeUVUUbLx1SlaVkkiNChgDzP1IM6OL8GCEJtyYfVS7lL0IW3xKw== benjamin.klum@helgoboss.org

EXPOSE 22

CMD ["/bootstrap.sh"]