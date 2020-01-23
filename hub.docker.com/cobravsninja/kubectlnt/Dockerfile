FROM datadog/docker-dd-agent
MAINTAINER support@tutum.co

# Output of: yaml2json tutum.yml | tr "\n" " " | sed 's/"/\\"/g'
LABEL co.tutum.yml="{   \"datadog\": {     \"image\": \"tutum/datadog-agent\",     \"restart\": \"on-failure\",     \"privileged\": true,     \"volumes\": [       \"/var/run/docker.sock:/var/run/docker.sock\",       \"/proc:/host/proc:ro\",       \"/sys/fs/cgroup:/host/sys/fs/cgroup:ro\"     ],     \"environment\": [       \"HOSTNAME=$TUTUM_NODE_HOSTNAME\",       \"64b9c0afcea4940746506697bd9849f4\"     ],     \"deployment_strategy\": \"every_node\"   } }"
