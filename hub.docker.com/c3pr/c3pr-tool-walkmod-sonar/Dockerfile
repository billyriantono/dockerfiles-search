#
# RUNTIME FOR THE TOOL
# Sets the basic environment where the tool (and the projects it supports) will run.
#
FROM maven:3-jdk-8-alpine

# NOTE: While we are under development, one RUN per line is better. When done, using "&& \" to group related lines is a better practice
RUN apk add --update wget nano unzip git

RUN mkdir -p /c3pr/project /c3pr/temp /c3pr/agent

#
#
# TOOL DOWNLOAD AND INSTALATION
# This adds the tool binary to the PATH. Also does any configuration specific to the tool.
#
#
RUN wget -O /c3pr/temp/walkmod.zip https://bitbucket.org/rpau/walkmod/downloads/walkmod-3.0.0-installer.zip
RUN unzip /c3pr/temp/walkmod.zip -d /c3pr/temp/walkmod
RUN mv /c3pr/temp/walkmod/walkmod-3.0.0 /c3pr/tool
# add it to path
ENV PATH="/c3pr/tool/bin:${PATH}"
# Pre-install all plugins to speed-up execution
ADD walkmod.xml /c3pr/temp/walkmod.xml
WORKDIR /c3pr/temp
RUN walkmod install
ADD pom.xml /c3pr/temp/pom.xml
RUN walkmod apply
RUN rm /c3pr/temp/pom.xml


#
#
# TOOL METADATA FOR C-3PR AGENT
# This one file (or many files) that contains the arguments for the tools this dockerfile provides.
# Basically this files tells what extensions (e.g. "java", "js") this tool can be executed on,
# what is the actual command the agent should execute to invoke the tool (e.g. "prettify --file #{filename}")
# and what should be the text of the PRs created as result of this tool.
#
#
RUN mkdir -p /c3pr/agent/tools
ENV C3PR_AGENT_TOOLS_PATH=/c3pr/agent/tools
COPY tools /c3pr/agent/tools

#
#
# DOWNLOAD C-3PR AGENT
# The agent is the program that will register this tool with the C-3PR hub while it is online; will also listen to
# tool invocation requests emitted by the c3pr-brain; will clone the repository before the tool execution; will
# execute the tool on the folder where the repo was cloned; will pick up any diffs and request a PR a creation.
#
#
RUN wget -O /c3pr/agent/c3pr-agent https://github.com/c3pr/c3pr-agent/releases/download/7.1.0/c3pr-agent-alpine-7.1.0
RUN chmod +x /c3pr/agent/c3pr-agent

EXPOSE 5003
ENV C3PR_AGENT_MAX_CONCURRENT_EXECUTIONS=5

ENTRYPOINT /c3pr/agent/c3pr-agent

