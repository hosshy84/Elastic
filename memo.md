# Install
```
docker network create elasticsearch --driver bridge
docker run -itd \
    -e "http.host=0.0.0.0" \
    -e "transport.host=127.0.0.1" \
    -e "xpack.security.enabled=false" \
    -e "xpack.monitoring.enabled=false" \
    -e "xpack.watcher.enabled=false" \
    -e "xpack.graph.enabled=false" \
    -e "xpack.ml.enabled=false" \
    -e "ES_JAVA_OPTS=-Xms512m -Xmx512m" \
    -p 9200:9200 \
    -p 9300:9300 \
    --name elasticsearch \
    --network="elasticsearch" \
    docker.elastic.co/elasticsearch/elasticsearch:6.1.1
docker run -itd \
    --name kibana \
    -p 5601:5601 \
    -e "ELASTICSEARCH_URL=http://elasticsearch:9200" \
    -e "xpack.graph.enabled=false" \
    -e "xpack.security.enabled=false" \
    -e "xpack.ml.enabled=false" \
    --network="elasticsearch" \
    docker.elastic.co/kibana/kibana:6.1.1
```