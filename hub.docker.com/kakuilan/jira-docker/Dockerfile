FROM cptactionhank/atlassian-jira-software:7.13.1

MAINTAINER kakuilan kakuilan@163.com

USER root

# agent version
ENV AGENT_VER=1.2.2

# get agent and set env
RUN wget https://github.com/pengzhile/atlassian-agent/releases/download/v${AGENT_VER}/atlassian-agent-v${AGENT_VER}.tar.gz \
  && tar xzf atlassian-agent-v${AGENT_VER}.tar.gz \
  && cp atlassian-agent-v${AGENT_VER}/atlassian-agent.jar /opt/atlassian/jira \
  && sed -i 's@^export JAVA_OPTS@export JAVA_OPTS="-javaagent:/opt/atlassian/jira/atlassian-agent.jar ${JAVA_OPTS}"@' /opt/atlassian/jira/bin/setenv.sh \
  && rm -rf atlassian-agent-v${AGENT_VER}*
