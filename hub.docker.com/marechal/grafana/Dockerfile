FROM grafana/grafana
RUN grafana-cli plugins list-remote | grep -i 'version:' | grep -i 'id:' | sed -E 's/version:.*//g' | sed -E 's/id:\s*//g' |  tr '\n' '\0' | xargs -0 -n1 grafana-cli plugins install 
