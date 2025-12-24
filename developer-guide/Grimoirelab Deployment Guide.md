1. [Grimoirelab  Deployment Documentation](#grimoirelab-deployment-documentation)
   1. [Introduction](#introduction)
   2. [Environment](#environment)
   3. [Pre-Requirements](#pre-requirements)
      1. [Basic Software Installation](#basic-software-installation)
   4. [Basic Components Deployment](#basic-components-deployment)
      1. [OpenSearch Deployment](#opensearch-deployment)
      2. [MariaDB Deployment](#mariadb-deployment)
   5. [Compass Metrics Model Component Deployment](#compass-metrics-model-component-deployment)
      1. [Related Repositories](#related-repositories)
      2. [Compass metrics model](#compass-metrics-model)

<a id="org88f0194"></a>

# Grimoirelab  Deployment Documentation

<a id="orgc510719"></a>

## Introduction

This document lists the Grimoirelab  dependencies and basic deployment steps for the service, as well as a description of the relevant configurations

<a id="org72e6319"></a> 

## Environment

-   Ubuntu 20.02
-   Python 3.8

<a id="org35c9fe2"></a>

## Pre-Requirements

<a id="org3ff7119"></a>

### Basic Software Installation

1.  python 3.8
    
    ```bash
    # install python3.8
    sudo apt-get update
    sudo apt-get install python3.8
    sudo apt-get install python3-pip
    sudo apt-get install python3-dev
    python3 --version
    ```
    
1.  Docker
    
    ```bash
    # setup docker sh
    # setup repository
    sudo apt-get update
    sudo apt-get install \
         ca-certificates \
         curl \
         gnupg \
         lsb-release
    
    # addd gpg key
    sudo mkdir -p /etc/apt/keyrings
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
    
    # setup gpg and repository
    echo \
    "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
    $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    
    # install docker engine
    sudo apt-get update
    sudo apt-get install docker-ce docker-ce-cli containerd.io
    ```
    
2.  docker-compose
    
    ```bash
    # install docker compose
    sudo apt-get update
    sudo apt-get install docker-compose-plugin docker-compose
    ```
    
3.  git
    
    ```bash
    # install git
    sudo apt-get update
    sudo apt-get git
    ```
    
     

<a id="org1a21d6d"></a>

## Basic Components Deployment

Basic components to rely on：

-   OpenSearch
    Used for Github/Gitee platform raw data / enrich data, and model report data storage.
    
-   MariaDB
    We'll create two databases later in the deployment:
    
    1.  compass<sub>saas</sub>: Compass business data storage, including user information, subscription information, Lab data and other Compass platform business data
    2.  compass<sub>director</sub>: Compass scheduler task data storage, including task parameters, task status, task details, etc.
    
    


<a id="org8da0943"></a>

### OpenSearch Deployment

You can refer to or use our docker-compose to deploy or manually go to opensearch and download the corresponding binary package for deployment.
1. Set enough virtual memory to secure OpenSearch  up[(reference)](https://github.com/chaoss/grimoirelab-sirmordred/blob/master/Getting-Started.md#low-virtual-memory-):

    option 1: `sysctl -w vm.max_map_count=262144`  that is only valid for current session.
    option 2: update `vm.max_map_count` setting in `/etc/sysctl.conf`.


2.  docker-compose [(refer to docker-compose-opensearch.yml](https://github.com/oss-compass/compass-web-service/blob/main/docker/docker-compose-opensearch-gitee.yml)) (Recommended)
    
    ```yml
    version: '3'
    services:
      opensearch-node1:
        image: opensearchproject/opensearch:1.3.4
        container_name: opensearch-node1
        environment:
          - cluster.name=opensearch-cluster
          - node.name=opensearch-node1
          - discovery.seed_hosts=opensearch-node1,opensearch-node2
          - cluster.initial_master_nodes=opensearch-node1,opensearch-node2
          - bootstrap.memory_lock=true # along with the memlock settings below, disables swapping
          - "OPENSEARCH_JAVA_OPTS=-Xms512m -Xmx512m" # minimum and maximum Java heap size, recommend setting both to 50% of system RAM
          - plugins.security.ssl.http.enabled=false  # disable ssl
        ulimits:
          memlock:
            soft: -1
            hard: -1
          nofile:
            soft: 65536 # maximum number of open files for the OpenSearch user, set to at least 65536 on modern systems
            hard: 65536
        volumes:
          - opensearch-data1:/usr/share/opensearch/data
        ports:
          - 9200:9200
          - 9600:9600 # required for Performance Analyzer
        networks:
          - opensearch-net
      opensearch-node2:
        image: opensearchproject/opensearch:1.3.4
        container_name: opensearch-node2
        environment:
          - cluster.name=opensearch-cluster
          - node.name=opensearch-node2
          - discovery.seed_hosts=opensearch-node1,opensearch-node2
          - cluster.initial_master_nodes=opensearch-node1,opensearch-node2
          - bootstrap.memory_lock=true
          - "OPENSEARCH_JAVA_OPTS=-Xms512m -Xmx512m"
        ulimits:
          memlock:
            soft: -1
            hard: -1
          nofile:
            soft: 65536
            hard: 65536
        volumes:
          - opensearch-data2:/usr/share/opensearch/data
        networks:
          - opensearch-net
      opensearch-dashboards:
        image: opensearchproject/opensearch-dashboards:1.3.4
        container_name: opensearch-dashboards
        ports:
          - 7601:5601
        expose:
          - "5601"
        environment:
          OPENSEARCH_HOSTS: '["https://opensearch-node1:9200","https://opensearch-node2:9200"]'
        networks:
          - opensearch-net
      hatstall:
        image: grimoirelab/hatstall:latest
        environment:
          - DATABASE_DIR=/db/
          - ADMIN_USER=admin
          - ADMIN_PASS=admin
        ports:
          - 8000:80
        links:
          - mariadb
        volumes:
          - ../default-grimoirelab-settings/apache-hatstall.conf:/home/grimoirelab/apache-hatstall.conf
          - ../default-grimoirelab-settings/shdb.cfg:/home/grimoirelab/shdb.cfg
    
    volumes:
      opensearch-data1:
      opensearch-data2:
    
    networks:
      opensearch-net:
    
    ```
    
    -  Create docker-compose-opensearch.yml file, and run it
    
        ```bash
        vi docker-compose-opensearch.yml  # copy docker-compose contents
        docker-compose -f docker-compose-opensearch.yml up -d
        ```
    
2.  (optional) Here's a document for you on how to manually setup an opensearch cluster.
    [How to configure openSearch cluster?](https://github.com/open-metrics-code/grimoirelab/wiki/How-to-configure-openSearch-cluster%3F)

    

<a id="org60a8fd8"></a>

### MariaDB Deployment

1.  docker-compose [(refer to docker-compose-opensearch.yml](https://github.com/oss-compass/compass-web-service/blob/main/docker/docker-compose-opensearch-gitee.yml)) (Recommended)
    
    ```yml
    version: '3'
    services:
      mariadb:
        image: mariadb:10.4.26
        expose:
          - 3306
        ports:
          - 3306:3306
        environment:
          - MYSQL_ROOT_PASSWORD=root
          - MYSQL_ALLOW_EMPTY_PASSWORD=yes
          - MYSQL_DATABASE=demo_sh
    ```


2.  Create docker-compose-mariadb.yml file, and run it

    ```bash
    vi docker-compose-mariadb.yml  # copy docker-compose contents
    docker-compose -f docker-compose-mariadb.yml up -d
    ```

<a id="orgb7707ea"></a>

## Compass Metrics Model Component Deployment


<a id="orgd6c980a"></a>

### Related Repositories

- [https://github.com/open-metrics-code](https://github.com/open-metrics-code)
- [https://github.com/oss-compass/compass-metrics-model](https://github.com/oss-compass/compass-metrics-model)


<a id="orgec0a053"></a>

2.  Install Compass customized Grimoirelab components

    1.  grimoirelab-elk
        
        ```bash
        $ pip3 uninstall grimoire-elk
        $ cd /data/repos
        $ git clone https://github.com/open-metrics-code/grimoirelab-elk
        $ cd grimoirelab-elk
        $ python3 setup.py develop
        ```

        You could check if grimoire-elk was intalled seccessfully by pip3 list:
        
            grimoire-elk        0.86.0     /data/repos/grimoireelk
    2.  grimoirelab-perceval
    
        ```bash
        $ pip3 uninstall perceval
        $ cd /data/repos
        $ git clone https://github.com/open-metrics-code/grimoirelab-perceval
        $ cd grimoirelab-perceval
        $ python3 setup.py develop
        ```
        
        You could check if grimoirelab-perceval was intalled seccessfully by pip3 list:
        
            perceval           0.20.0rc3  /data/repos/perceval
    3.  grimoirelab-elk-gitee
        
        ```bash
        $ cd /data/repos
        $ git clone https://github.com/open-metrics-code/grimoirelab-elk-gitee
        $ cd grimoirelab-elk-gitee
        $ python3 setup.py develop
        ```
        
        You could check if grimoirelab-elk-gitee was intalled seccessfully by pip3 list:
        
            grimoire-elk-gitee       0.1.0       /data/repos/grimoirelab-elk-gitee
    4.  grimoirelab-perceval-gitee
        
        ```bash
        $ cd /data/repos
        $ git clone https://github.com/open-metrics-code/grimoirelab-perceval-gitee
        $ cd grimoirelab-perceval-gitee
        $ python3 setup.py develop
        ```
        
        You could check if grimoirelab-perceval-gitee was intalled seccessfully by pip3 list:
        
            perceval-gitee      0.1.0       /data/repos/grimoirelab-perceval-gitee


<a id="org9ed58d2"></a>

### Compass metrics model

Install compass metrics model

```bash
$ cd /data/repos
$ git clone https://github.com/oss-compass/compass-metrics-model
$ cd compass-metrics-model
$ python3 setup.py develop
```

You could check if compass-metrics-model was intalled seccessfully by pip3 list:
        
    compass-metrics-model         0.1.0       /data/repos/compass-metrics-model







