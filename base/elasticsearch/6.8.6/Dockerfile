FROM openjdk:8-jre

LABEL maintainer="phithon <root@leavesongs.com>"

ARG ESHOME=/usr/share/elasticsearch
ADD docker-entrypoint.sh /

RUN set -ex \
    && mkdir -p ${ESHOME} \
    && wget -qO- https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-6.8.6.tar.gz | tar zx \
        --strip-components 1 -C ${ESHOME} \
    && chmod +x /docker-entrypoint.sh

ENV PATH ${ESHOME}/bin:$PATH
WORKDIR ${ESHOME}
EXPOSE 9200 9300

ADD elasticsearch.yml ./config/
RUN sed -ex \
    && chown nobody:nogroup -R ${ESHOME}

USER nobody:nogroup
ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["elasticsearch"]