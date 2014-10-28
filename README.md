## ElasticSearch Beta Dockerfile

This repository contains **Dockerfile** of the latest beta release of [ElasticSearch](http://www.elasticsearch.org/) for Docker. 

The corresponding Docker registry repo is here: (https://registry.hub.docker.com/u/eliotk/elasticsearch-beta/)

The Docker registry repo is an automated build repo so that the images will always reflect what's in the Dockerfile.

This is based on the official [Docker elasticsearch repo](https://registry.hub.docker.com/u/dockerfile/elasticsearch/).

### Base Docker Image

* [dockerfile/java:oracle-java7](http://dockerfile.github.io/#/java)


### Installation

1. Install [Docker](https://www.docker.com/).

2. Download [automated build](https://registry.hub.docker.com/u/dockerfile/elasticsearch/) from public [Docker Hub Registry](https://registry.hub.docker.com/): `docker pull eliotk/elasticsearch-beta`

   (alternatively, you can build an image from Dockerfile: `docker build -t="eliotk/elasticsearch-beta" github.com/eliotk/elasticsearch-docker-beta`)


### Usage

    docker run -d -p 9200:9200 -p 9300:9300 eliotk/elasticsearch-beta

#### Attach persistent/shared directories

  1. Create a mountable data directory `<data-dir>` on the host.

  2. Create ElasticSearch config file at `<data-dir>/elasticsearch.yml`.

    ```yml
    path:
      logs: /data/log
      data: /data/data
    ```

  3. Start a container by mounting data directory and specifying the custom configuration file:

    ```sh
    docker run -d -p 9200:9200 -p 9300:9300 -v <data-dir>:/data eliotk/elasticsearch /elasticsearch/bin/elasticsearch -Des.config=/data/elasticsearch.yml
    ```

After few seconds, open `http://<host>:9200` to see the result.
