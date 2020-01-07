FROM alpine
VOLUME /mnt

# WARNING you have Transparent Huge Pages (THP) support enabled in your kernel.
#   This will create latency and memory usage issues with Redis.
#   To fix this issue run the command 'echo never > /sys/kernel/mm/transparent_hugepage/enabled' as root,
#   and add it to your /etc/rc.local in order to retain the setting after a reboot.
#   Redis must be restarted after THP is disabled.

RUN echo "echo never > /sys/kernel/mm/transparent_hugepage/enabled" >> /fix-issues.sh
RUN echo "echo never > /sys/kernel/mm/transparent_hugepage/defrag" >> /fix-issues.sh
RUN echo "echo 1 > /mnt/vm/overcommit_memory" >> /fix-issues.sh
RUN chmod 777 /fix-issues.sh

CMD /fix-issues.sh
