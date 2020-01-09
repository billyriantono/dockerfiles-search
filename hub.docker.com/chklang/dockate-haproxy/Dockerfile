FROM node:8-alpine
WORKDIR /dockate
RUN (npm install @dockate/core@1.0.6 || 0) && \
        (npm install dockate-haproxy@1.0.7 || 0) && \
        echo "#!/bin/sh" > /dockate/run.sh && \
        echo "ERRORS=" >> /dockate/run.sh && \
        echo "if [[ -z \"\$INTERVAL_BETWEEN_CHECK\" ]]; then" >> /dockate/run.sh && \
        echo "  export INTERVAL_BETWEEN_CHECK=5000" >> /dockate/run.sh && \
        echo "fi" >> /dockate/run.sh && \
        echo "if [[ -z \"\$SWARM_HOST\" ]]; then" >> /dockate/run.sh && \
        echo "  export ERRORS=\"\$ERRORS\\\nSWARM_HOST not defined\"" >> /dockate/run.sh && \
        echo "fi" >> /dockate/run.sh && \
        echo "if [[ -z \"\$SWARM_PORT_HTTP\" ]]; then" >> /dockate/run.sh && \
        echo "  export ERRORS=\"\$ERRORS\\\nSWARM_PORT_HTTP not defined\"" >> /dockate/run.sh && \
        echo "fi" >> /dockate/run.sh && \
        echo "if [[ -z \"\$SWARM_PORT_SSH\" ]]; then" >> /dockate/run.sh && \
        echo "  export ERRORS=\"\$ERRORS\\\nSWARM_PORT_SSH not defined\"" >> /dockate/run.sh && \
        echo "fi" >> /dockate/run.sh && \
        echo "if [[ -z \"\$SWARM_USERNAME\" ]]; then" >> /dockate/run.sh && \
        echo "  export ERRORS=\"\$ERRORS\\\nSWARM_USERNAME not defined\"" >> /dockate/run.sh && \
        echo "fi" >> /dockate/run.sh && \
        echo "if [[ -z \"\$SWARM_PASSWORD\" ]]; then" >> /dockate/run.sh && \
        echo "  export ERRORS=\"\$ERRORS\\\nSWARM_PASSWORD not defined\"" >> /dockate/run.sh && \
        echo "fi" >> /dockate/run.sh && \
        echo "if [[ -z \"\$HAPROXY_HOST\" ]]; then" >> /dockate/run.sh && \
        echo "  export ERRORS=\"\$ERRORS\\\nHAPROXY_HOST not defined\"" >> /dockate/run.sh && \
        echo "fi" >> /dockate/run.sh && \
        echo "if [[ -z \"\$HAPROXY_PORT_SSH\" ]]; then" >> /dockate/run.sh && \
        echo "  export ERRORS=\"\$ERRORS\\\nHAPROXY_PORT_SSH not defined\"" >> /dockate/run.sh && \
        echo "fi" >> /dockate/run.sh && \
        echo "if [[ -z \"\$HAPROXY_USERNAME_SSH\" ]]; then" >> /dockate/run.sh && \
        echo "  export ERRORS=\"\$ERRORS\\\nHAPROXY_USERNAME_SSH not defined\"" >> /dockate/run.sh && \
        echo "fi" >> /dockate/run.sh && \
        echo "if [[ -z \"\$HAPROXY_PASSWORD_SSH\" ]]; then" >> /dockate/run.sh && \
        echo "  export ERRORS=\"\$ERRORS\\\nHAPROXY_PASSWORD_SSH not defined\"" >> /dockate/run.sh && \
        echo "fi" >> /dockate/run.sh && \
        echo "if [[ -z \"\$HAPROXY_FOLDER\" ]]; then" >> /dockate/run.sh && \
        echo "  export ERRORS=\"\$ERRORS\\\nHAPROXY_FOLDER not defined\"" >> /dockate/run.sh && \
        echo "fi" >> /dockate/run.sh && \
        echo "if [[ -z \"\$HAPROXY_HTTP_PORT\" ]]; then" >> /dockate/run.sh && \
        echo "  export ERRORS=\"\$ERRORS\\\nHAPROXY_HTTP_PORT not defined\"" >> /dockate/run.sh && \
        echo "fi" >> /dockate/run.sh && \
        echo "if [[ -z \"\$HAPROXY_HTTPS_PORT\" ]]; then" >> /dockate/run.sh && \
        echo "  export ERRORS=\"\$ERRORS\\\nHAPROXY_HTTPS_PORT not defined\"" >> /dockate/run.sh && \
        echo "fi" >> /dockate/run.sh && \
        echo "if [[ -z \"\$HAPROXY_FORCE_HTTPS\" ]]; then" >> /dockate/run.sh && \
        echo "  export HAPROXY_FORCE_HTTPS=false" >> /dockate/run.sh && \
        echo "fi" >> /dockate/run.sh && \
        echo "if [[ -z \"\$HAPROXY_CERTIFICATS_PATH\" ]]; then" >> /dockate/run.sh && \
        echo "  export HAPROXY_CERTIFICATS_PATH=" >> /dockate/run.sh && \
        echo "fi" >> /dockate/run.sh && \
        echo "if [[ -z \"\$HAPROXY_RELOAD_COMMAND\" ]]; then" >> /dockate/run.sh && \
        echo "  export ERRORS=\"\$ERRORS\\\nHAPROXY_RELOAD_COMMAND not defined\"" >> /dockate/run.sh && \
        echo "fi" >> /dockate/run.sh && \
        echo "if [[ -z \"\$HAPROXY_USE_CAT\" ]]; then" >> /dockate/run.sh && \
        echo "  export HAPROXY_USE_CAT=false" >> /dockate/run.sh && \
        echo "fi" >> /dockate/run.sh && \
        echo "if [[ -z \"\$ERRORS\" ]]; then" >> /dockate/run.sh && \
        echo "  echo \"Script OK, run...\"" >> /dockate/run.sh && \
        echo "else" >> /dockate/run.sh && \
        echo "  echo -e ERRORS : \$ERRORS" >> /dockate/run.sh && \
        echo "  exit 1" >> /dockate/run.sh && \
        echo "fi" >> /dockate/run.sh && \
        echo "node node_modules/@dockate/core/lib/exec.js \\" >> /dockate/run.sh && \
        echo "  --dockerproxy.intervalBetweenCheckServices \"\$INTERVAL_BETWEEN_CHECK\" \\" >> /dockate/run.sh && \
        echo "  --dockerproxy.swarmHost \"\$SWARM_HOST\" \\" >> /dockate/run.sh && \
        echo "  --dockerproxy.swarmPortHTTP \"\$SWARM_PORT_HTTP\" \\" >> /dockate/run.sh && \
        echo "  --dockerproxy.swarmPortSSH \"\$SWARM_PORT_SSH\" \\" >> /dockate/run.sh && \
        echo "  --dockerproxy.swarmUsername \"\$SWARM_USERNAME\" \\" >> /dockate/run.sh && \
        echo "  --dockerproxy.swarmPassword \"\$SWARM_PASSWORD\" \\" >> /dockate/run.sh && \
        echo "  --dockerproxy.webservice \"file://node_modules/dockate-haproxy/lib/haproxy.js\" \\" >> /dockate/run.sh && \
        echo "  --dockerproxy.haProxyHost \"\$HAPROXY_HOST\" \\" >> /dockate/run.sh && \
        echo "  --dockerproxy.haProxyPort \"\$HAPROXY_PORT_SSH\" \\" >> /dockate/run.sh && \
        echo "  --dockerproxy.haProxyUsername \"\$HAPROXY_USERNAME_SSH\" \\" >> /dockate/run.sh && \
        echo "  --dockerproxy.haProxyPassword \"\$HAPROXY_PASSWORD_SSH\" \\" >> /dockate/run.sh && \
        echo "  --dockerproxy.haProxyFolder \"\$HAPROXY_FOLDER\" \\" >> /dockate/run.sh && \
        echo "  --dockerproxy.haProxyHTTPPort \"\$HAPROXY_HTTP_PORT\" \\" >> /dockate/run.sh && \
        echo "  --dockerproxy.haProxyHTTPSPort \"\$HAPROXY_HTTPS_PORT\" \\" >> /dockate/run.sh && \
        echo "  --dockerproxy.haProxyForceHTTPS \"\$HAPROXY_FORCE_HTTPS\" \\" >> /dockate/run.sh && \
        echo "  --dockerproxy.haProxySSLCertificatsPath \"\$HAPROXY_CERTIFICATS_PATH\" \\" >> /dockate/run.sh && \
        echo "  --dockerproxy.haProxyReloadCommand \"\$HAPROXY_RELOAD_COMMAND\" \\" >> /dockate/run.sh && \
        echo "  --dockerproxy.haProxyUseCAT \"\$HAPROXY_USE_CAT\"" >> /dockate/run.sh && \
        chmod +x /dockate/run.sh
CMD /dockate/run.sh
