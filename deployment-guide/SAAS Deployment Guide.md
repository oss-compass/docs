
# Table of Contents

- [Table of Contents](#table-of-contents)
- [Compass SAAS Deployment Documentation](#compass-saas-deployment-documentation)
  - [Introduction](#introduction)
    - [Architecture](#architecture)
    - [Environment](#environment)
  - [Pre-Requirements](#pre-requirements)
    - [Basic Software Installation](#basic-software-installation)
    - [Setup Compass Project Information Repository and Webhooks](#setup-compass-project-information-repository-and-webhooks)
    - [Setup OAuth Apps](#setup-oauth-apps)
    - [Setup Mail server](#setup-mail-server)
    - [Setup S3 Storage](#setup-s3-storage)
  - [Basic Components Deployment](#basic-components-deployment)
    - [OpenSearch Deployment](#opensearch-deployment)
    - [MariaDB Deployment](#mariadb-deployment)
    - [RabbitMQ Deployment](#rabbitmq-deployment)
    - [Redis Deployment](#redis-deployment)
  - [Compass Metrics Model Component Deployment](#compass-metrics-model-component-deployment)
    - [Related Repositories](#related-repositories)
    - [Grimoirelab](#grimoirelab)
    - [Compass metrics model](#compass-metrics-model)
  - [Compass Scheduler Component Deployment](#compass-scheduler-component-deployment)
    - [Repository](#repository)
    - [Python Requirements](#python-requirements)
    - [Install from source](#install-from-source)
    - [Configure the scheduler](#configure-the-scheduler)
    - [Run scheduler](#run-scheduler)
  - [Compass SVG Render Component Deployment](#compass-svg-render-component-deployment)
    - [Repository](#repository-1)
    - [Overview](#overview)
    - [Build with Docker](#build-with-docker)
  - [Compass Backend Service Deployment](#compass-backend-service-deployment)
    - [Repository](#repository-2)
    - [Install RVM and Ruby, Official website installation link](#install-rvm-and-ruby-official-website-installation-link)
    - [Install dependencies](#install-dependencies)
    - [Configure env file](#configure-env-file)
    - [Setting up the projects information Submodule](#setting-up-the-projects-information-submodule)
    - [Run Service](#run-service)
  - [Compass Frontend Service Deployment](#compass-frontend-service-deployment)
    - [Overview](#overview-1)
    - [Build with Docker](#build-with-docker-1)
  - [Compass Gateway Service Deployment](#compass-gateway-service-deployment)
    - [Overview](#overview-2)
    - [Build with Docker](#build-with-docker-2)
  - [Final](#final)


<a id="org88f0194"></a>

# Compass SAAS Deployment Documentation


<a id="orgc510719"></a>

## Introduction

This document lists the Compass SAAS component dependencies and basic deployment steps for the service, as well as a description of the relevant configurations


<a id="org72e6319"></a>

### Architecture

![Architecture](Compass.arch.png)


<a id="orgbaba904"></a>

### Environment

-   Ubuntu 20.02


<a id="org35c9fe2"></a>

## Pre-Requirements


<a id="org3ff7119"></a>

### Basic Software Installation

1.  Docker
    
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

2.  docker-compose
    
        # install docker compose
        sudo apt-get update
        sudo apt-get install docker-compose-plugin docker-compose
3.  git
    
        # install git
        sudo apt-get update
        sudo apt-get git
4.  python
    
        # install python3.8
        sudo apt-get update
        sudo apt-get install python3.8
        sudo apt-get install python3-pip
        sudo apt-get install python3-dev
        python3 --version


<a id="orgcdd26c5"></a>

### Setup Compass Project Information Repository and Webhooks

1.  Overview

    You need to create a repository like [https://github.com/oss-compass/compass-projects-information](https://github.com/oss-compass/compass-projects-information)
    and set up a corresponding webhook to collect Compass SAAS project submitions.

2.  Webhook Settings

    About how to create a webhook you could refer to [https://docs.github.com/en/webhooks/using-webhooks/creating-webhooks](https://docs.github.com/en/webhooks/using-webhooks/creating-webhooks)
    
    -   Payload URL: https://[compass.host]/api/workflow
    -   Content type: application/json
    -   Secret: xxx
        You can create a random password, but please remember it, this password will be used later in the deployment of the other services.
    -   Which events would you like to trigger this webhook: Send me everything.


<a id="org3f8d84d"></a>

### Setup OAuth Apps

1.  Apply for Github OAuth application: [https://docs.github.com/en/apps/oauth-apps/building-oauth-apps/creating-an-oauth-app](https://docs.github.com/en/apps/oauth-apps/building-oauth-apps/creating-an-oauth-app)
    -   Homepage URL: https://[compass.host]
    -   Authorization callback URL: https://[compass.host]/users/auth/github/callback
2.  Apply for Gitee OAuth application: [https://gitee.com/api/v5/oauth_doc#/list-item-3](https://gitee.com/api/v5/oauth_doc#/list-item-3)
    -   Homepage URL: https://[compass.host]
    -   Authorization callback URL: https://[compass.host]/users/auth/gitee/callback
3.  Apply for Wechat OAuth application: [https://developers.weixin.qq.com/doc/oplatform/Website_App/WeChat_Login/Wechat_Login.html](https://developers.weixin.qq.com/doc/oplatform/Website_App/WeChat_Login/Wechat_Login.html)
4.  Apply for Slack OAuth application: [https://api.slack.com/legacy/oauth](https://api.slack.com/legacy/oauth)


<a id="orgb014291"></a>

### Setup Mail server

You need to apply for a mail and smtp server in advance to use as a sender for services such as registering users and notifications for OSS Compass.
For example: [https://support.google.com/a/answer/176600](https://support.google.com/a/answer/176600)


<a id="org93494c2"></a>

### Setup S3 Storage

You need to register an S3 storage service in advance to use as image upload and resource storage for OSS Compass.
For example: [https://aws.amazon.com/s3/](https://aws.amazon.com/s3/)


<a id="org1a21d6d"></a>

## Basic Components Deployment

Basic components to rely on:

-   OpenSearch
    Used for Github/Gitee platform raw data / enrich data, and model report data storage.
-   MariaDB
    We'll create two databases later in the deployment:
    1.  compass<sub>saas</sub>: Compass business data storage, including user information, subscription information, Lab data and other Compass platform business data
    2.  compass<sub>director</sub>: Compass scheduler task data storage, including task parameters, task status, task details, etc.
-   RabbitMQ
    Used for data interaction between back-end service and scheduling service, as well as for asynchronous task processing for back-end service.
-   Redis
    Used for back-end service caching including homepage trends, project badges, and task result caching for scheduling services.


<a id="org8da0943"></a>

### OpenSearch Deployment

You can refer to or use our docker-compose to deploy or manually go to opensearch and download the corresponding binary package for deployment.

1.  docker-compose [(refer to docker-compose-opensearch.yml](https://github.com/oss-compass/compass-web-service/blob/main/docker/docker-compose-opensearch-gitee.yml)) (Recommended)
    
        version: '3'
        services:
          opensearch-node1:
            image: opensearchproject/opensearch:1.3.4
            container_name: opensearch-node1
            environment:
              - cluster.name=opensearch-cluster
              - node.name=opensearch-node1
              - discovery.seed_hosts=opensearch-node1,opensearch-node2,opensearch-node3
              - cluster.initial_master_nodes=opensearch-node1,opensearch-node2,opensearch-node3
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
              - 8200:9200
              - 9600:9600 # required for Performance Analyzer
            networks:
              - opensearch-net
          opensearch-node2:
            image: opensearchproject/opensearch:1.3.4
            container_name: opensearch-node2
            environment:
              - cluster.name=opensearch-cluster
              - node.name=opensearch-node2
              - discovery.seed_hosts=opensearch-node1,opensearch-node2,opensearch-node3
              - cluster.initial_master_nodes=opensearch-node1,opensearch-node2,opensearch-node3
              - bootstrap.memory_lock=true
              - "OPENSEARCH_JAVA_OPTS=-Xms512m -Xmx512m"
              - plugins.security.ssl.http.enabled=false  # disable ssl
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
          opensearch-node3:
            image: opensearchproject/opensearch:1.3.4
            container_name: opensearch-node3
            environment:
              - cluster.name=opensearch-cluster
              - node.name=opensearch-node3
              - discovery.seed_hosts=opensearch-node1,opensearch-node2,opensearch-node3
              - cluster.initial_master_nodes=opensearch-node1,opensearch-node2,opensearch-node3
              - bootstrap.memory_lock=true
              - "OPENSEARCH_JAVA_OPTS=-Xms512m -Xmx512m"
              - plugins.security.ssl.http.enabled=false  # disable ssl
            ulimits:
              memlock:
                soft: -1
                hard: -1
              nofile:
                soft: 65536
                hard: 65536
            volumes:
              - opensearch-data3:/usr/share/opensearch/data
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
              OPENSEARCH_HOSTS: '["https://opensearch-node1:9200","https://opensearch-node2:9200","https://opensearch-node3:9200"]'
            networks:
              - opensearch-net
        volumes:
          opensearch-data1:
          opensearch-data2:
          opensearch-data3:
        networks:
          opensearch-net:

    -  Create docker-compose-opensearch.yml file, and run it

            vi docker-compose-opensearch.yml  # copy docker-compose contents
            docker-compose -f docker-compose-opensearch.yml up -d

2.  (optional) Here's a document for you on how to manually setup an opensearch cluster.
    [How to configure openSearch cluster?](https://github.com/open-metrics-code/grimoirelab/wiki/How-to-configure-openSearch-cluster%3F)

3.  Set enough virtual memory to secure OpenSearch up ([reference](https://github.com/chaoss/grimoirelab-sirmordred/blob/master/Getting-Started.md#low-virtual-memory-)):
    -   option 1: `sysctl -w vm.max_map_count=262144` that is only valid for current session.
    -   option 2: update `vm.max_map_count` setting in `/etc/sysctl.conf`, run `sudo sysctl -p` to validate the configuration file .


<a id="org60a8fd8"></a>

### MariaDB Deployment

1.  docker-compose [(refer to docker-compose-opensearch.yml](https://github.com/oss-compass/compass-web-service/blob/main/docker/docker-compose-opensearch-gitee.yml)) (Recommended)
    
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


2.  Create docker-compose-mariadb.yml file, and run it

        vi docker-compose-mariadb.yml  # copy docker-compose contents
        docker-compose -f docker-compose-mariadb.yml up -d

<a id="orgb7707ea"></a>

### RabbitMQ Deployment

1.  docker-compose (Recommended)
    
        version: '3'
        services:
          rabbitmq1:
            image: rabbitmq:3-management
            environment:
              - RABBITMQ_ERLANG_COOKIE=cookie
              - RABBITMQ_DEFAULT_USER=rabbitmq_user
              - RABBITMQ_DEFAULT_PASS=rabbitmq_pass
              - RABBITMQ_DEFAULT_VHOST=/
            ports:
              - 4369:4369
              - 5672:5672
              - 15672:15672
              - 25672:25672
              - 35672:35672

2.  Create docker-compose-rabbitmq.yml file, and run it

        vi docker-compose-rabbitmq.yml  # copy docker-compose contents
        docker-compose -f docker-compose-rabbitmq.yml up -d

<a id="org972617a"></a>

### Redis Deployment

1.  docker-compose (Recommended)
    
        version: '3'
        services:
           redis:
             image: redis:latest
             ports:
               - "6379:6379"
             volumes:
               - ./redis.conf:/etc/redis/redis.conf
               - ./data:/data
             command: redis-server /etc/redis/redis.conf
             privileged: true
2.  Redis conf
    
        bind 0.0.0.0
        protected-mode yes
        port 6379
        tcp-backlog 511
        daemonize no
        supervised no
        pidfile /var/run/redis_6379.pid
        loglevel notice
        logfile ""
        databases 16
        always-show-logo yes
        save 900 1
        save 300 10
        save 60 10000
        stop-writes-on-bgsave-error yes
        rdbcompression yes
        rdbchecksum yes
        dbfilename dump.rdb
        replica-serve-stale-data yes
        repl-diskless-sync no
        repl-diskless-sync-delay 5
        repl-diskless-load disabled
        repl-disable-tcp-nodelay no
        replica-priority 100
        acllog-max-len 128
        lazyfree-lazy-eviction no
        lazyfree-lazy-expire no
        lazyfree-lazy-server-del no
        replica-lazy-flush no
        lazyfree-lazy-user-del no
        oom-score-adj no
        oom-score-adj-values 0 200 800
        appendonly no
        appendfilename "appendonly.aof"
        appendfsync everysec
        no-appendfsync-on-rewrite no
        auto-aof-rewrite-percentage 100
        auto-aof-rewrite-min-size 64mb
        aof-load-truncated yes
        aof-use-rdb-preamble yes
        lua-time-limit 5000
        slowlog-log-slower-than 10000
        slowlog-max-len 128
        latency-monitor-threshold 0
        notify-keyspace-events ""
        hash-max-ziplist-entries 512
        hash-max-ziplist-value 64
        list-max-ziplist-size -2
        list-compress-depth 0
        set-max-intset-entries 512
        zset-max-ziplist-entries 128
        zset-max-ziplist-value 64
        hll-sparse-max-bytes 3000
        stream-node-max-bytes 4096
        stream-node-max-entries 100
        activerehashing yes
        client-output-buffer-limit normal 0 0 0
        client-output-buffer-limit replica 256mb 64mb 60
        client-output-buffer-limit pubsub 32mb 8mb 60
        hz 10
        dynamic-hz yes
        aof-rewrite-incremental-fsync yes
        rdb-save-incremental-fsync yes
        jemalloc-bg-thread yes
        requirepass redis_pass  #redis pass

3.  Create docker-compose-redis.yml file, and run it

        vi docker-compose-redis.yml  # copy docker-compose contents
        vi redis.conf # # copy redis conf contents
        docker-compose -f docker-compose-redis.yml up -d

<a id="orgcb8f479"></a>

## Compass Metrics Model Component Deployment


<a id="orgd6c980a"></a>

### Related Repositories

- [https://github.com/open-metrics-code](https://github.com/open-metrics-code)
- [https://github.com/oss-compass/compass-metrics-model](https://github.com/oss-compass/compass-metrics-model)


<a id="orgec0a053"></a>

### Grimoirelab

referenced from [How to run grimoirelab?](https://github.com/open-metrics-code/grimoirelab/wiki/How-to-run-grimoirelab-gitee%3F)

1.  Build from source

    Build all modules by the latest release of GrimoireLab:
    
        $ sudo apt-get install libmysqlclient-dev
        $ git clone https://github.com/open-metrics-code/grimoirelab
        $ cd ~/grimoirelab/utils
        $ mkdir /data/repos
        $ mkdir -p /data/tmp && touch /data/tmp/log
        $ ./build_grimoirelab -l debug --logfile /data/tmp/log --build --install --check --relfile ../releases/latest --reposdir /data/repos --install_system

2.  Install Compass customized Grimoirelab components

    1.  grimoirelab-elk
        
            $ pip3 uninstall grimoire-elk
            $ cd /data/repos
            $ git clone https://github.com/open-metrics-code/grimoirelab-elk
            $ cd grimoirelab-elk
            $ python3 setup.py develop
        
        You could check if grimoire-elk was intalled seccessfully by pip3 list:

            grimoire-elk        0.86.0     /data/repos/grimoireelk
    2.  grimoirelab-perceval

            $ pip3 uninstall perceval
            $ cd /data/repos
            $ git clone https://github.com/open-metrics-code/grimoirelab-perceval
            $ cd grimoirelab-perceval
            $ python3 setup.py develop
        
        You could check if grimoirelab-perceval was intalled seccessfully by pip3 list:
        
            perceval           0.20.0rc3  /data/repos/perceval
    3.  grimoirelab-elk-gitee
        
            $ cd /data/repos
            $ git clone https://github.com/open-metrics-code/grimoirelab-elk-gitee
            $ cd grimoirelab-elk-gitee
            $ python3 setup.py develop

        You could check if grimoirelab-elk-gitee was intalled seccessfully by pip3 list:
        
            grimoire-elk-gitee       0.1.0       /data/repos/grimoirelab-elk-gitee
    4.  grimoirelab-perceval-gitee
        
            $ cd /data/repos
            $ git clone https://github.com/open-metrics-code/grimoirelab-perceval-gitee
            $ cd grimoirelab-perceval-gitee
            $ python3 setup.py develop
        
        You could check if grimoirelab-perceval-gitee was intalled seccessfully by pip3 list:
        
            perceval-gitee      0.1.0       /data/repos/grimoirelab-perceval-gitee


<a id="org9ed58d2"></a>

### Compass metrics model

Install compass metrics model

    $ cd /data/repos
    $ git clone https://github.com/oss-compass/compass-metrics-model
    $ cd compass-metrics-model
    $ python3 setup.py develop

You could check if compass-metrics-model was intalled seccessfully by pip3 list:
        
    compass-metrics-model         0.1.0       /data/repos/compass-metrics-model


<a id="org7497042"></a>

## Compass Scheduler Component Deployment


<a id="org51976f6"></a>

### Repository

[https://github.com/oss-compass/compass-service-scheduler](https://github.com/oss-compass/compass-service-scheduler)


<a id="org56b0653"></a>

### Python Requirements

please use pip install follow packages:

-   celery-director
-   pendulum
-   tldextract
-   urllib3==1.26.5
-   requests==2.26.0
-   pyyaml==6.0


<a id="orgb440785"></a>

### Install from source

    $ git clone https://github.com/oss-compass/compass-service-scheduler
    $ cd compass-service-scheduler
    $ git submodule init
    $ git submodule update
    $ cd celery-director
    $ python -m pip install -i .


<a id="org1c42624"></a>

### Configure the scheduler

1.  create database manually: `compass_director`
2.  Update `.env` file According to the comments in the following example
    
        
        # ---------- Database ----------
        DIRECTOR_DATABASE_URI="mysql+mysqlconnector://user:pass@host:3306/compass_director"
        DIRECTOR_SAAS_DATABASE_URI="mysql+mysqlconnector://user:pass@host:3306/compass_saas"
        DIRECTOR_DATABASE_POOL_RECYCLE=600
        
        # ---------- Celery ----------
        DIRECTOR_BROKER_URI="amqp://admin:admin@localhost" # RabbitMQ
        DIRECTOR_RABBITMQ_URI="amqp://admin:admin@localhost"  # RabbitMQ
        DIRECTOR_RESULT_BACKEND_URI="redis://:redis_pass@localhost:6379/0" # Redis
        
        # ---------- Frontend ----------
        DIRECTOR_API_URL="http://0.0.0.0:8000/api"
        DIRECTOR_FLOWER_URL="http://0.0.0.0:5555" # Optional
        DIRECTOR_ENABLE_HISTORY_MODE=false
        DIRECTOR_REFRESH_INTERVAL=30000
        
        # ---------- API ----------
        DIRECTOR_WORKFLOWS_PER_PAGE=100
        DIRECTOR_AUTH_ENABLED = false
        
        DIRECTOR_ENABLE_CDN=false
        DIRECTOR_STATIC_FOLDER=${DIRECTOR_HOME}/static
        
        # ---------- Sentry ----------
        DIRECTOR_SENTRY_DSN=""
        
        # ---------- Retention ----------
        DIRECTOR_DEFAULT_RETENTION_OFFSET=-1
        
        # ---------- Custom ----------
        DIRECTOR_GITEE_API_TOKEN=[gitee_token1, gitee_token2]
        DIRECTOR_GITHUB_API_TOKEN=[github_token1, github_token2]
        DIRECTOR_GRIMOIRELAB_CONFIG_FOLDER="/path/to/compass-service-scheduler/analysis_data"
        DIRECTOR_GRIMOIRELAB_CONFIG_TEMPLATE="/path/to/compass-service-scheduler/setup-template.cfg"
        
        DIRECTOR_GITHUB_PROXY=          # Proxy
        DIRECTOR_ES_URL="http://admin:admin@opensearch:8200"  # OpenSearch
        DIRECTOR_METRICS_OUT_INDEX="compass_model"            # Index prefix for Compass metrics model
        DIRECTOR_METRICS_FROM_DATE="2000-01-01"               # Default FROM_DATE
        DIRECTOR_METRICS_LEVEL="repo"                         # Default level
        DIRECTOR_HOOK_PASS="Webhook Password the previously created"                 # Webhook Password for callback validation
        DIRECTOR_IDENTITIES_CONFIG_FILE="/path/to/compass-metrics-model/compass_contributor/conf_utils/identities.yml"
        DIRECTOR_ORGANIZATIONS_CONFIG_FILE="/path/to/compass-metrics-model/compass_contributor/conf_utils/organizations.json"
        DIRECTOR_BOTS_CONFIG_FILE="/path/to/compass-metrics-model/compass_contributor/conf_utils/bots.json"
3.  db migration:
    
        $ export DIRECTOR_HOME=/path/to/compass-service-scheduler 
        $ director db upgrade


<a id="orgb6dc770"></a>

### Run scheduler

    $ export DIRECTOR_HOME=/path/to/compass-service-scheduler
    
    ## Web Service UI
    
    $ director webserver
    
    ### or listen to 0.0.0.0
    
    $ director webserver -b 0.0.0.0:8000
    
    ## Celery Worker
    
    $ director celery worker --loglevel=info --queues=analyze_queue_v1,analyze_queue_v2,custom_queue_v1 --concurrency 32


<a id="org062c49a"></a>

## Compass SVG Render Component Deployment


<a id="org944a728"></a>

### Repository

[https://github.com/oss-compass/compass-echarts-server](https://github.com/oss-compass/compass-echarts-server)


<a id="org304d050"></a>

### Overview

This Component is a echarts server side render by node canvas, using for generating chart image by Echarts.


<a id="orgf75af06"></a>

### Build with Docker 

1.  docker-compose
    
        version: '3'
        services:
          echarts-server:
            build:
              context: .
              dockerfile: Dockerfile
            ports:
              - "8084:8081"
            extra_hosts:
              - "host.docker.internal:host-gateway"
2.  Dockerfile
    
        FROM node:16-alpine AS base
        # # If your server node is in a special area, you can replace the apk source to speed up deployment. For example as follow:
        # RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.tuna.tsinghua.edu.cn/g' /etc/apk/repositories
        # RUN apk update
        RUN apk add --no-cache build-base tzdata  cairo-dev jpeg-dev pango-dev freetype-dev giflib-dev&& \
            cp -r -f /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
        
        RUN npm install -g pm2
        
        FROM base AS final
        WORKDIR /root/
        COPY ./ /root
        RUN npm install --unsafe-perm --canvas_binary_host_mirror=https://registry.npmmirror.com/-/binary/canvas/
        EXPOSE 8081
        CMD ["pm2-docker", "start", "server.js"]

3.  run compass svg

        git clone git@github.com:oss-compass/compass-echarts-server.git
        cd compass-echarts-server
        docker-compose -f docker-compose.yml up -d

<a id="org19fa82a"></a>

## Compass Backend Service Deployment


<a id="org287719a"></a>

### Repository

[https://github.com/oss-compass/compass-web-service](https://github.com/oss-compass/compass-web-service)


<a id="org9ac5d4a"></a>

### Install RVM and Ruby, [Official website installation link](https://github.com/rvm/ubuntu_rvm)

    sudo apt install gnupg2
    gpg2 --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
    \curl -sSL https://get.rvm.io | bash -s stable
    source /home/git/.rvm/scripts/rvm
    rvm install 3.1.2


<a id="org8cba87f"></a>

### Install dependencies

    sudo apt install libmysqlclient-dev
    git clone https://github.com/oss-compass/compass-web-service
    cd compass-web-service
    bundle install


<a id="orgfce23ae"></a>

### Configure env file

1.  cp .env.example .env
2.  update `.env` According to the following example
    
        export RAILS_ENV=production
        
        ## Host
        export DEFAULT_HOST=https://host-for-compass
        
        ## Mariadb (Do not use the same database as the scheduler service)
        export MARIADB_PORT=3306
        export MARIADB_USER=user
        export MARIADB_PASSWORD=pass
        export MARIADB_DB=compass_saas
        export MARIADB_POOL=100
        
        ## RabbitMQ
        export MQ_CONNECTION=amqp://admin:admin@localhost
        
        ## Redis URL
        export REDIS_URL=redis://:redis_pass@redis:6379/1
        export REDIS_CHANNEL_PREFIX=compass-web-service
        
        ## Admin web
        export ADMIN_WEB_USERNAME=admin_user
        export ADMIN_WEB_PASSWORD=admin_pass
        export ADMIN_WEB_TOKEN=
        # export ADMIN_SLACK_WEBBHOOK= # Official working group slack channel callbacks webhook
        
        ## Secret keys
        # You can use `rake secret` command to generate a secret key
        export DEVISE_JWT_SECRET_KEY=my-jwt-secret-key
        
        ## Opensearch
        export OPENSEARCH_URL=http://localhost:9200
        export OPENSEARCH_USER=user
        export OPENSEARCH_PASS=pass
        
        ## Celery Server
        export CELERY_SERVER=http://localhost:8000
        export METRICS_OUT_INDEX=compass_model
        
        ## WebHook
        export HOOK_PASS=password
        export WORKFLOW_REPO_NAME=compass-projects-information
        export GITEE_WORKFLOW_REPO=https://gitee.com/oss-compass/compass-projects-information
        export GITHUB_WORKFLOW_REPO=https://github.com/oss-compass/compass-projects-information
        
        ## Robot
        export GITEE_API_TOKEN=robot_api_access_token
        export GITHUB_API_TOKEN=robot_api_access_token
        
        ## Proxy
        export PROXY=
        
        ## OmniAuth gitee
        export GITEE_CLIENT_ID=gitee_client_id
        export GITEE_CLIENT_SECRET=gitee_client_secret
        export GITEE_SCOPE='user_info'
        
        ## OmniAuth github
        export GITHUB_CLIENT_ID=github_client_id
        export GITHUB_CLIENT_SECRET=github_client_secret
        export GITHUB_SCOPE='user'
        
        ## OmniAuth slack
        export SLACK_CLIENT_ID=slack_client_id
        export SLACK_CLIENT_SECRET=slack_client_secret
        export SLACK_CLIENT_JWK_SIGNING_KEY=slack_client_jwk_signing_key
        export SLACK_SCOPE='openid email profile'
        export SLACK_API_TOKEN=slack_api_token
        
        ## OmniAuth wechat
        export WECHAT_CLIENT_ID=wechat_client_id
        export WECHAT_CLIENT_SECRET=wechat_client
        export WECHAT_SCOPE=snsapi_base
        export WECHAT_TOKEN=wechat_token
        export WECHAT_SUBSCRIBE_LINK=https://compass.gitee.com/settings/profile
        
        # Mail
        export MAIL_HOST=smtp.163.com
        export MAIL_PORT=465
        export MAIL_SSL=true
        export MAIL_SECURE=true
        export MAIL_USER=mail_user
        export MAIL_FROM=mail_from
        export MAIL_PASSWORD=mailing_password
        export MAIL_TIMEOUT=15

        ## Yahoo Template
        # export MAIL_HOST=smtp.mail.yahoo.com
        # export MAIL_PORT=465
        # export MAIL_SSL=true
        # export MAIL_SECURE=true
        # export MAIL_AUTH=plain
        # export MAIL_USER=mail_user
        # export MAIL_FROM=mail_from
        # export MAIL_PASSWORD=mailing_password
        # export MAIL_TIMEOUT=15

        ## Gmail Template
        # export MAIL_HOST=smtp.gmail.com
        # export MAIL_PORT=587
        # export MAIL_SSL=false
        # export MAIL_SECURE=true
        # export MAIL_AUTH=plain
        # export MAIL_USER=mail_user
        # export MAIL_FROM=mail_from
        # export MAIL_PASSWORD=mail_application_specific_password ## https://support.google.com/accounts/answer/185833?sjid=16410464921634023198-AP
        # export MAIL_TIMEOUT=15
        
        # Email limit
        export MAX_EMAIL_CHANGE_COUNT=3
        # Send Email limit
        export MAX_SEND_EMAIL_COUNT=3
        
        ## S3 Storage
        export S3_ENDPOINT=https://aws
        export S3_ACCESS_KEY_ID=your_access_key_id
        export S3_SECRET_KEY=your_secret_key
        export S3_REGION=us-east
        export S3_BUCKET=your_bucket_name
        
        ## Kafka Censoring (Optional)
        # export KAFKA_SERVERS=127.0.0.1:9092
        # export KAFKA_ACKS=1
        # export KAFKA_USERNAME=username
        # export KAFKA_PASSWORD=password
        # export KAFKA_MECHANISM=SCRAM-SHA-256
        
        # ## Censoring flag
        # export CENSORING_ENABLE=false
        
        # Notification
        export NOTIFICATION_URL=https://oss-compass.org
        export NOTIFICATION_ZH_URL=https://compass.gitee.com
        export NOTIFICATION_ANALYZE_URL=/analyze
        export NOTIFICATION_ABOUT_URL=/docs/community
        export NOTIFICATION_SUBSCRIPTION_URL=/settings/subscribe
        export NOTIFICATION_EXPLORE_URL=/explore
        
        # Notification Wechat Template
        # export NOTIFICATION_WECHAT_ACCOUNT_BIND_TEMPLATE_ID=wechat template id
        # export NOTIFICATION_WECHAT_REPORT_GENERATE_TEMPLATE_ID=wechat template id
        # export NOTIFICATION_WECHAT_REPORT_SUBSCRIPTION_UPDATE_TEMPLATE_ID=wechat template id
        
        # CI Bots
        export BOT_NAME=compass-bot
        export BOT_EMAIL=compass-bot@gitee.com
        
        # OpenTelemetry (Optional)
        export OTEL_EXPORTER=otlp
        export OTEL_SERVICE_NAME=CompassSAAS
        export OTEL_EXPORTER_OTLP_ENDPOINT=http://localhost:4318
        export OTEL_RESOURCE_ATTRIBUTES=application=compass-web-service
        
        # Lab
        export LAB_MODEL_TRIGGER_COUNT=5
        
        # Protected Reports
        export RESTRICTED_LABEL_LIST=oss-compass
        export RESTRICTED_LABEL_VIEWERS=2
        
        # other servers
        export ECHARTS_SERVER=http://127.0.0.1:8084 # SVG Render Component Server URL
3.  db migrate (create tables for compass web service)
    
        $ cd compass-web-service
        $ rails db:migrate
        $ rails db:seed
4.  initializate secret
    
        $ RAILS_ENV=prodcution bundle exec rake secret
        # => xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx (copy the secert)
        $ bin/rails credentials:edit
        # => Fill in the secret copied above and save & exit edit
        # If the key is wrong, delete the previous one: rm config/credentials.yml.enc 


<a id="org39d23a5"></a>

### Setting up the projects information Submodule

```bash
$ cd compass-web-service
$ git submodule init
$ git submodule update 
$ cd compass-projects-information
$ git remote set-url origin <your-information-repository-url>
```


<a id="org1402d62"></a>

### Run Service

```bash
# Assets Precompile
$ RAILS_ENV=production bundle exec rake assets:precompile

# Run Web services
$ cd compass-web-service
$ bundle exec rails s -e production -b 0.0.0.0

# Run Asynchronous Task services
$ cd compass-web-service
$ bundle exec rake rabbitmq:start

# Run Scheduled Task services
$ cd compass-web-service
$ bundle exec crono -e production
```


<a id="org83b7463"></a>

## Compass Frontend Service Deployment


<a id="org7f2e27b"></a>

### Overview

This is a frontend project for the oss compass, including official website and metric chart pages. Built using the popular front-end framework Next.js, and connected to the backend with graphql for data integration.
compass-web: [https://github.com/oss-compass/compass-web](https://github.com/oss-compass/compass-web)
compass-docs: [https://github.com/oss-compass/document-website](https://github.com/oss-compass/document-website)


<a id="org9969347"></a>

### Build with Docker

1.  docker-compose

    ```yaml
    version: '3'
    services:
      docs-server:
        image: registry.cn-hongkong.aliyuncs.com/oss-compass/compass-docs:nightly
        ports:
          - "8081:3000"
      next-server:
        image: registry.cn-hongkong.aliyuncs.com/oss-compass/compass-web:nightly
        env_file: .env
        volumes:
          - .env:/app/.env
        ports:
          - "8082:3000"
        extra_hosts:
          - "host.docker.internal:host-gateway"
    ```

2.  Dockerfile for compass-web

    ```dockerfile
    FROM node:16-alpine AS builder
    # # If your server node is in a special area, you can replace the apk source to speed up deployment. For example as follow:
    # RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.tuna.tsinghua.edu.cn/g' /etc/apk/repositories
    RUN apk add --no-cache git libc6-compat
    
    WORKDIR /oss-compass
    
    ARG REGISTRY
    
    COPY ["package.json", "yarn.lock", "./"]
    
    COPY ./apps apps
    COPY ./packages packages
    
    RUN if [[ -z "$REGISTRY" ]] ; then echo not set registry ; else yarn config set registry $REGISTRY && npm config set registry $REGISTRY ; fi
    RUN yarn config list
    RUN yarn
    
    # Next.js collects completely anonymous telemetry data about general usage.
    # Learn more here: https://nextjs.org/telemetry
    # Uncomment the following line in case you want to disable telemetry during the build.
    ENV NEXT_TELEMETRY_DISABLED 1
    ENV SENTRY_LOG_ENABLE 1
    
    # custom env
    ARG GIT_COMMIT
    ARG SENTRY_DSN
    ARG SENTRY_AUTH_TOKEN
    
    ENV NEXT_PUBLIC_GIT_COMMIT=$GIT_COMMIT
    ENV SENTRY_RELEASE=$GIT_COMMIT
    
    ENV SENTRY_DSN=$SENTRY_DSN
    ENV NEXT_PUBLIC_SENTRY_DSN=$SENTRY_DSN
    
    ENV SENTRY_AUTH_TOKEN=$SENTRY_AUTH_TOKEN
    
    COPY . .
    
    RUN yarn build
    
    # If using npm comment out above and use below instead
    # RUN npm run build
    
    # Production image, copy all the files and run next
    FROM node:16-alpine AS runner
    WORKDIR /oss-compass
    
    ENV NODE_ENV production
    # Uncomment the following line in case you want to disable telemetry during runtime.
    ENV NEXT_TELEMETRY_DISABLED 1
    
    # custom env
    ARG GIT_COMMIT
    ARG SENTRY_DSN
    
    ENV NEXT_PUBLIC_GIT_COMMIT=$GIT_COMMIT
    ENV SENTRY_RELEASE=$GIT_COMMIT
    
    ENV SENTRY_DSN=$SENTRY_DSN
    ENV NEXT_PUBLIC_SENTRY_DSN=$SENTRY_DSN
    
    RUN addgroup --system --gid 1001 nodejs
    RUN adduser --system --uid 1001 nextjs
    
    COPY --from=builder /oss-compass/apps/web/next.config.js .
    COPY --from=builder /oss-compass/apps/web/package.json .
    
    # Automatically leverage output traces to reduce image size
    # https://nextjs.org/docs/advanced-features/output-file-tracing
    COPY --from=builder --chown=nextjs:nodejs /oss-compass/apps/web/.next/standalone ./
    COPY --from=builder --chown=nextjs:nodejs /oss-compass/apps/web/.next/static ./apps/web/.next/static
    COPY --from=builder --chown=nextjs:nodejs /oss-compass/apps/web/public ./apps/web/public
    
    USER nextjs
    
    EXPOSE 3000
    
    ENV PORT 3000
    
    CMD ["node", "apps/web/server.js"]
    ```

3.  Dockerfile for compass-doc

    ```dockerfile
    FROM nginx:1.23.2-alpine
    
    COPY build /usr/share/nginx/html/build
    COPY nginx.conf /etc/nginx/conf.d/default.conf
    EXPOSE 3000
    
    ENTRYPOINT ["nginx", "-g", "daemon off;"]
    ```

4.  Create docker-compose-compassweb.yml file, and run it

    ```bash
    cd compass-web-service
    vi docker-compose-compassweb.yml  # copy docker-compose contents
    docker-compose -f docker-compose-compassweb.yml up -d
    ```


<a id="org32f44e3"></a>

## Compass Gateway Service Deployment


<a id="org486aec7"></a>

### Overview

Compass uses nginx as the gateway entry point for the entire service, which is distributed to the different services via route matching.


<a id="orgca6e24a"></a>

### Build with Docker

1.  docker-compose

    ```yaml
    version: '3'
    services:
      nginx:
        image: nginx:1.23.3
        restart: always
        ports:
          - "80:80"
        volumes:
          - ./nginx/nginx.conf:/etc/nginx/nginx.conf
          - ./nginx/server.conf:/etc/nginx/conf.d/default.conf
        extra_hosts:
          - "host.docker.internal:host-gateway"
    ```

2.  nginx.conf

    ```nginx
    user  nginx;
    worker_processes  auto;
    
    error_log  /var/log/nginx/error.log notice;
    pid        /var/run/nginx.pid;
    
    
    events {
        worker_connections  1024;
    }
    
    
    http {
        include       /etc/nginx/mime.types;
        default_type  application/octet-stream;
    
        log_format  main  '\$remote_addr - \$remote_user [\$time_local] "\$request" '
                          '\$status \$body_bytes_sent "\$http_referer" '
                          '"\$http_user_agent" "\$http_x_forwarded_for"';
    
        access_log  /var/log/nginx/access.log  main;
    
        #limit_req_zone \$binary_remote_addr zone=compassperipreq:100m rate=1000r/s;
        #limit_req_status 429;
        #limit_req zone=compassperipreq burst=5;
    
        sendfile        on;
        #tcp_nopush     on;
    
        keepalive_timeout  65;
    
        #gzip  on;
    
        include /etc/nginx/conf.d/*.conf;
    }
    ```

3.  server.conf

    ```nginx
    server {
             listen 80;
             server_name _;
             client_max_body_size 100M;
             client_body_buffer_size     32k;
             client_header_buffer_size   16k;
             large_client_header_buffers 8 64k;
    
             location /zh/ {
                 proxy_set_header Host \$host;
                 proxy_set_header X-Real-IP \$remote_addr;
                 proxy_set_header X-Forwarded-For \$proxy_add_x_forwarded_for;
                 proxy_pass http://host.docker.internal:8081/zh/;
             }
    
             location /docs/ {
                 proxy_set_header Host \$host;
                 proxy_set_header X-Real-IP \$remote_addr;
                 proxy_set_header X-Forwarded-For \$proxy_add_x_forwarded_for;
                 proxy_pass http://host.docker.internal:8081/docs/;
             }
             location /blog/ {
                 proxy_set_header Host \$host;
                 proxy_set_header X-Real-IP \$remote_addr;
                 proxy_set_header X-Forwarded-For \$proxy_add_x_forwarded_for;
                 proxy_pass http://host.docker.internal:8081/blog/;
             }
             location /assets/ {
                 proxy_set_header Host \$host;
                 proxy_set_header X-Real-IP \$remote_addr;
                 proxy_set_header X-Forwarded-For \$proxy_add_x_forwarded_for;
                 proxy_pass http://host.docker.internal:8081/assets/;
             }
             location /img/ {
                 proxy_set_header Host \$host;
                 proxy_set_header X-Real-IP \$remote_addr;
                 proxy_set_header X-Forwarded-For \$proxy_add_x_forwarded_for;
                 proxy_pass http://host.docker.internal:8081/img/;
             }
             location /404 {
                 proxy_set_header Host \$host;
                 proxy_set_header X-Real-IP \$remote_addr;
                 proxy_set_header X-Forwarded-For \$proxy_add_x_forwarded_for;
                 proxy_pass http://host.docker.internal:8081/404;
             }
    
             location /api/hook {
                 proxy_set_header Host \$host;
                 proxy_set_header X-Real-IP \$remote_addr;
                 proxy_set_header X-Forwarded-For \$proxy_add_x_forwarded_for;
                 proxy_pass http://host.docker.internal:3000/api/hook;
             }
             location /api/graphql {
                 proxy_set_header Host \$host;
                 proxy_set_header X-Real-IP \$remote_addr;
                 proxy_set_header X-Forwarded-For \$proxy_add_x_forwarded_for;
                 proxy_pass http://host.docker.internal:3000/api/graphql;
             }
             location /api/workflow {
                 proxy_set_header Host \$host;
                 proxy_set_header X-Real-IP \$remote_addr;
                 proxy_set_header X-Forwarded-For \$proxy_add_x_forwarded_for;
                 proxy_pass http://host.docker.internal:3000/api/worflow;
             }
             location /users {
                 proxy_set_header Host \$host;
                 proxy_set_header X-Real-IP \$remote_addr;
                 proxy_set_header X-Forwarded-For \$proxy_add_x_forwarded_for;
                 proxy_pass http://host.docker.internal:3000/users;
             }
             location /badge {
                 proxy_set_header Host \$host;
                 proxy_set_header X-Real-IP \$remote_addr;
                 proxy_set_header X-Forwarded-For \$proxy_add_x_forwarded_for;
                 proxy_pass http://host.docker.internal:3000/badge;
             }
             location /chart {
                 proxy_set_header Host \$host;
                 proxy_set_header X-Real-IP \$remote_addr;
                 proxy_set_header X-Forwarded-For \$proxy_add_x_forwarded_for;
                 proxy_pass http://host.docker.internal:3000/chart;
    
             }
             location /files {
                 proxy_set_header Host \$host;
                 proxy_set_header X-Real-IP \$remote_addr;
                 proxy_set_header X-Forwarded-For \$proxy_add_x_forwarded_for;
                 proxy_pass http://host.docker.internal:3000/files;
             }
             location / {
                 proxy_set_header Host \$host;
                 proxy_set_header X-Real-IP \$remote_addr;
                 proxy_set_header X-Forwarded-For \$proxy_add_x_forwarded_for;
                 proxy_pass http://host.docker.internal:8082/;
             }
         }
    ```

4.  Create docker-compose-nginx.yml file, and run it

    ```bash
    mkdir nginx
    cd nginx 
    vi nginx.conf   # copy nginx conf contents
    vi server.conf   # copy server conf contents
    cd ../
    vi docker-compose-nginx.yml  # copy docker-compose contents
    docker-compose -f docker-compose-nginx.yml up -d
    ```

<a id="orgf07ef65"></a>

## Final

After deploying the gateway, basically the entire Compass SAAS Service is deployed, enjoy it!

    https://oss-compass-host/   # oss-compass home page
    https://oss-compass-host:8000/#/   #oss-compass director
    https://oss-compass-host:15672/    #oss-compass rabbitmq


