# LICENSE CDDL 1.0 + GPL 2.0
#
# DOCKERFILE FOR ORACLE DB 11g
# --------------------------

FROM wnameless/oracle-xe-11g:latest

ADD assets/ /tmp/assets/

RUN chmod +x /tmp/assets/setup.sh && /tmp/assets/setup.sh && rm -rf /tmp/assets

