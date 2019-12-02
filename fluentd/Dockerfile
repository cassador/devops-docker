FROM fluent/fluentd:v1.6.0-debian-1.0

USER root

RUN buildDeps="sudo make gcc g++ libc-dev" \
 && apt-get update \
 && apt-get install -y --no-install-recommends $buildDeps \
 && sudo gem install fluent-plugin-aws-elasticsearch-service \
 && sudo gem install fluent-plugin-secure-forward \
 && sudo gem install fluent-plugin-record-reformer \
 && sudo gem install fluent-plugin-kubernetes_metadata_filter \
 && sudo gem install fluent-plugin-grok-parser \
 && sudo gem install fluent-plugin-concat \
 && sudo gem sources --clear-all \
 && SUDO_FORCE_REMOVE=yes \
    apt-get purge -y --auto-remove \
                  -o APT::AutoRemove::RecommendsImportant=false \
                  $buildDeps \
 && rm -rf /var/lib/apt/lists/* \
 && rm -rf /tmp/* /var/tmp/* /usr/lib/ruby/gems/*/cache/*.gem

# COPY fluent.conf /fluentd/etc/
# COPY kubernetes_reduced.conf /fluentd/etc/kubernetes.conf
# COPY entrypoint.sh /bin/

# RUN chmod +x /bin/entrypoint.sh

# USER fluent