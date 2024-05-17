

Docker compost YML file
``` Docker compost YML
version: '3.5'

services:
  tubearchivist:
    container_name: tubearchivist
    restart: unless-stopped
    image: bbilly1/tubearchivist
    ports:
      - 8050:8000
    volumes:
      - /media/goliath/ext/docker/tubearchivist/youtube:/youtube
      - /home/goliath/docker/tubearchivist/cache:/cache
    environment:
      - ES_URL=http://archivist-es:9200     # needs protocol e.g. http and port
      - REDIS_HOST=archivist-redis          # don't add protocol
      - HOST_UID=1000
      - HOST_GID=1000
      - TA_HOST=192.168.29.198:8050
      - TA_USERNAME=tubearchivist           # your initial TA credentials
      - TA_PASSWORD=verysecret              # your initial TA credentials
      - ELASTIC_PASSWORD=verysecret         # set password for Elasticsearch
      - TZ=Asia/Kolkata
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:8000/health"]
      interval: 2m
      timeout: 10s
      retries: 3
      start_period: 30s
    depends_on:
      - archivist-es
      - archivist-redis
    networks:
      - tubearchivist

  archivist-redis:
    image: redis/redis-stack-server
    container_name: archivist-redis
    restart: unless-stopped
    expose:
      - "6379"
    volumes:
      - redis:/data
    depends_on:
      - archivist-es
    networks:
      - tubearchivist

  archivist-es:
    image: bbilly1/tubearchivist-es         # only for amd64, or use official es 8.13.2
    container_name: archivist-es
    restart: unless-stopped
    environment:
      - "ELASTIC_PASSWORD=verysecret"       # matching Elasticsearch password
      - "ES_JAVA_OPTS=-Xms512m -Xmx512m"
      - "xpack.security.enabled=true"
      - "discovery.type=single-node"
      - "path.repo=/usr/share/elasticsearch/data/snapshot"
    ulimits:
      memlock:
        soft: -1
        hard: -1
    volumes:
      - /home/goliath/docker/tubearchivist/es:/usr/share/elasticsearch/data    # check for permission error when using bind mount, see readme
    expose:
      - "9200"
    networks:
      - tubearchivist

networks:
  tubearchivist:
    driver: bridge

volumes:
  media:
  cache:
  redis:
  es:
```
