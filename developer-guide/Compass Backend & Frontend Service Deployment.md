 1. [Compass Backend Service Deployment](#compass-backend-service-deployment)
      1. [Repository](#repository)
      2. [Install RVM and Ruby, [Official website installation link](https://github.com/rvm/ubuntu_rvm)](#install-rvm-and-ruby-official-website-installation-linkhttpsgithubcomrvmubuntu_rvm)
      3. [Install dependencies](#install-dependencies)
      4. [Configure env file](#configure-env-file)
      5. [Setting up the projects information Submodule](#setting-up-the-projects-information-submodule)
      6. [Run Service](#run-service)
 2. [Compass Frontend Service Deployment](#compass-frontend-service-deployment)
      1. [Overview](#overview)
      2. [Build with Docker](#build-with-docker)
 3. [Compass Gateway Service Deployment](#compass-gateway-service-deployment)
      1. [Overview](#overview)
      2. [Build with Docker](#build-with-docker)
  4. [Run Scheduled Task services](#run-scheduled-task-services)
      1. [Compass Frontend Service Deployment](#compass-frontend-service-deployment)
         1. [Overview](#overview)
         2. [Build with Docker](#build-with-docker)
      2. [Compass Gateway Service Deployment](#compass-gateway-service-deployment)
         1. [Overview](#overview)
         2. [Build with Docker](#build-with-docker)
      3. [Compass Scheduler Component Deployment](#compass-scheduler-component-deployment)
         1. [Repository](#repository)
         2. [Python Requirements](#python-requirements)
         3. [Install from source](#install-from-source)
         4. [Configure the scheduler](#configure-the-scheduler)
         5. [Run scheduler](#run-scheduler)
  5. [Final](#final)

<a id="org88f0194"></a>

##   Compass Backend Service Deployment


<a id="org287719a"></a>

### Repository

<https://github.com/oss-compass/compass-web-service>


<a id="org9ac5d4a"></a>

### Install RVM and Ruby, [Official website installation link](https://github.com/rvm/ubuntu_rvm)

```bash
sudo apt install gnupg2
gpg2 --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
\curl -sSL https://get.rvm.io | bash -s stable
source /home/git/.rvm/scripts/rvm
rvm install 3.1.2
```


<a id="org8cba87f"></a>

### Install dependencies

```bash
sudo apt install libmysqlclient-dev
git clone https://github.com/oss-compass/compass-web-service
cd compass-web-service
bundle install
```


<a id="orgfce23ae"></a>

### Configure env file

1.  cp .env.example .env
2.  update `.env` According to the following example
    
    ```
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
    ```
3.  db migrate (create tables for compass web service)
    
    ```bash
    $ cd compass-web-service
    $ rails db:migrate
    $ rails db:seed
    ```
4.  initializate secret
    
    ```bash
    $ RAILS_ENV=prodcution bundle exec rake secret
    # => xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx (copy the secert)
    $ bin/rails credentials:edit
    # => Fill in the secret copied above and save & exit edit
    # If the key is wrong, delete the previous one: rm config/credentials.yml.enc 
    ```


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

##  Compass Frontend Service Deployment


<a id="org7f2e27b"></a>

### Overview

This is a frontend project for the oss compass, including official website and metric chart pages. Built using the popular front-end framework Next.js, and connected to the backend with graphql for data integration.
compass-web: <https://github.com/oss-compass/compass-web>
compass-docs: <https://github.com/oss-compass/document-website>

<a id="org9969347"></a>

### Build with Docker

1.  docker-compose
    
    ```yml
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
    
    ```yml
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
    
    ```yml
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
          
             log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                                '$status $body_bytes_sent "$http_referer" '
                                '"$http_user_agent" "$http_x_forwarded_for"';
          
             access_log  /var/log/nginx/access.log  main;
        
             #limit_req_zone $binary_remote_addr zone=compassperipreq:100m rate=1000r/s;
             #limit_req_status 429;
             #limit_req zone=compassperipreq burst=5;
         
             sendfile        on;
             #tcp_nopush     on; 
             keepalive_timeout  65;
        
             #gzip  on;
         
             include /etc/nginx/conf.d/*.conf;
         }
3.  server.conf
    
    ```
    server {
             listen 80;
             server_name _;
             client_max_body_size 100M;
             client_body_buffer_size     32k;
             client_header_buffer_size   16k;
             large_client_header_buffers 8 64k;
    
             location /zh/ {
                 proxy_set_header Host $host;
                 proxy_set_header X-Real-IP $remote_addr;
                 proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                 proxy_pass http://host.docker.internal:8081/zh/;
             }
    
             location /docs/ {
                 proxy_set_header Host $host;
                 proxy_set_header X-Real-IP $remote_addr;
                 proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                 proxy_pass http://host.docker.internal:8081/docs/;
             }
             location /blog/ {
                 proxy_set_header Host $host;
                 proxy_set_header X-Real-IP $remote_addr;
                 proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                 proxy_pass http://host.docker.internal:8081/blog/;
             }
             location /assets/ {
                 proxy_set_header Host $host;
                 proxy_set_header X-Real-IP $remote_addr;
                 proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                 proxy_pass http://host.docker.internal:8081/assets/;
             }
             location /img/ {
                 proxy_set_header Host $host;
                 proxy_set_header X-Real-IP $remote_addr;
                 proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                 proxy_pass http://host.docker.internal:8081/img/;
             }
             location /404 {
                 proxy_set_header Host $host;
                 proxy_set_header X-Real-IP $remote_addr;
                 proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                 proxy_pass http://host.docker.internal:8081/404;
             }
    
             location /api/hook {
                 proxy_set_header Host $host;
                 proxy_set_header X-Real-IP $remote_addr;
                 proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                 proxy_pass http://host.docker.internal:3000/api/hook;
             }
             location /api/graphql {
                 proxy_set_header Host $host;
                 proxy_set_header X-Real-IP $remote_addr;
                 proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                 proxy_pass http://host.docker.internal:3000/api/graphql;
             }
             location /api/workflow {
                 proxy_set_header Host $host;
                 proxy_set_header X-Real-IP $remote_addr;
                 proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                 proxy_pass http://host.docker.internal:3000/api/worflow;
             }
             location /users {
                 proxy_set_header Host $host;
                 proxy_set_header X-Real-IP $remote_addr;
                 proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                 proxy_pass http://host.docker.internal:3000/users;
             }
             location /badge {
                 proxy_set_header Host $host;
                 proxy_set_header X-Real-IP $remote_addr;
                 proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                 proxy_pass http://host.docker.internal:3000/badge;
             }
             location /chart {
                 proxy_set_header Host $host;
                 proxy_set_header X-Real-IP $remote_addr;
                 proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                 proxy_pass http://host.docker.internal:3000/chart;
    
             }
             location /files {
                 proxy_set_header Host $host;
                 proxy_set_header X-Real-IP $remote_addr;
                 proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                 proxy_pass http://host.docker.internal:3000/files;
             }
             location / {
                 proxy_set_header Host $host;
                 proxy_set_header X-Real-IP $remote_addr;
                 proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
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



<a id="org7497042"></a>

## Compass Scheduler Component Deployment


<a id="org51976f6"></a>

### Repository

<https://github.com/oss-compass/compass-service-scheduler>


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

```bash
$ git clone https://github.com/oss-compass/compass-service-scheduler
$ cd compass-service-scheduler
$ git submodule init
$ git submodule update
$ cd celery-director
$ python -m pip install -i .
```


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


<a id="orgf07ef65"></a>

## Final

After deploying the gateway, basically the  Compass backed and frontend Service is deployed, enjoy it!

    https://oss-compass-host/   # oss-compass home page
    https://oss-compass-host:8000/#/   #oss-compass director
    https://oss-compass-host:15672/    #oss-compass rabbitmq