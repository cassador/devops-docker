FROM fluent/fluentd:v1.6.0-debian-1.0

USER root

RUN buildDeps="sudo make gcc g++ libc-dev" 
RUN apt-get update 
RUN apt-get install -y --no-install-recommends $buildDeps 
#RUN gem install fluent-plugin-aws-elasticsearch-service 
RUN gem install fluent-plugin-secure-forward 
RUN gem install fluent-plugin-record-reformer 
RUN gem install fluent-plugin-kubernetes_metadata_filter 
RUN gem install fluent-plugin-grok-parser 
RUN gem install fluent-plugin-concat 
RUN gem sources --clear-all 
RUN SUDO_FORCE_REMOVE=yes \
    apt-get purge -y --auto-remove \
                  -o APT::AutoRemove::RecommendsImportant=false \
                  $buildDeps \
RUN rm -rf /var/lib/apt/lists/* 
RUN rm -rf /tmp/* /var/tmp/* /usr/lib/ruby/gems/*/cache/*.gem

# COPY fluent.conf /fluentd/etc/
# COPY kubernetes_reduced.conf /fluentd/etc/kubernetes.conf
# COPY entrypoint.sh /bin/

# RUN chmod +x /bin/entrypoint.sh

# USER fluent
