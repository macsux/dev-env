A collection of services to setup up local development environment via docker-compose. 

### How to use

Some services require unique configuration for your environment which is provided via .env files. Details are listed below

#### Start

```
docker-compose up -d <SERVICENAME...>
```

*You can specify more then one service name. Omit to start everything*

#### Stop

```
docker-compose down
```

### Included services:

#### Databases / Cache

- `mysql` - MySQL
  - Server: localhost:3306
  - Credentials: root / (blank)
  
- `redis` - Redis
  - localhost:6379

- `postgres` - PostgreSQL
  - Server: localhost:5432
  - Credentials: admin/admin

- `mongo` - MongoDB
  - Server: localhost:27017
  - Credentials: admin/admin

- `oracle` - [Oracle 12.2.0.1](https://www.influxdata.com/time-series-platform/telegraf/) 
  - localhost:1521  - Oracle listener
- SERVICE_NAME = ORCLPDB1.localdomain 
  - USERNAME = system 
  - PASSWORD = Oradoc_db1
  
- `sqlserver` - [SQL Server 2017 (Linux)]
  - localhost:1433
  - Credentials: sa/P@ssword

- `eventstore` - [EventStore](https://eventstore.org/)
  - Server: localhost:1113
  - Credentials: admin/changeit
  - UI: http://localhost:2113

- `axon-server` - [Axon Server](https://axoniq.io/product-overview/axon-server) 
  - http://localhost:8024 - admin UI
  - localhost:8124 - api

##### Messaging

- `rabbitmq` - [RabbitMQ](https://www.rabbitmq.com/)
  - Server: localhost:5672
  - Credentials: guest/guest
  - Management UI: http://localhost:8084


##### Admin UI

- `omnidb` - OmniDB - multi-db web based GUI (postgresql, mysql, oracle)
  - http://localhost:8085
  - Credentials: admin/admin
- Use service names as host address when setting up connection strings
  
- `redis-commander` - [Redis Commander](https://github.com/joeferner/redis-commander) - UI for redis  
  - http://localhost:8081

- `mongo-express` - [Mongo Express](https://github.com/mongo-express/mongo-express) (web based GUI)
  - http://localhost:8082

- `phpmyadmin` - [PhpMyAdmin](https://www.phpmyadmin.net/), UI to interact with `mysql` container
  - UI: http://localhost:8083

##### Spring Cloud Services

- `config-server` - [Spring Cloud Config Server](https://cloud.spring.io/spring-cloud-config) 
  - http://localhost:8888
  - By default looks for config files inside `./config` directory. Edit `config-server.env` to reconfigure to use Git
  
- `eureka` - [Spring Cloud Eureka](https://spring.io/projects/spring-cloud-netflix) 
  - http://localhost:8761
  
- `hystrix` - [Spring Cloud Circuit Breaker Dashboard](https://cloud.spring.io/spring-cloud-static/Edgware.SR6/multi/multi__circuit_breaker_hystrix_dashboard.html) 
  - http://localhost:7979

##### CI/CD  

- `concourse` - ConcourseCI
  - Server: http://localhost:8087
  - Credentials: test/test

##### Observability

- `zipkin` - Zipkin - distributed tracing  
  
  - http://localhost:9411
  
- `telegraf` - [Telegraf](https://www.influxdata.com/time-series-platform/telegraf/)   
  
  - Preconfigured to scrape prometheus endpoints in a host app and send them to wavefront. Edit `telegraf.conf` to adjust settings.
  
- `wavefront` - [Wavefront Proxy](https://docs.wavefront.com/proxies.html) 
  - localhost:2878 - metrics ingestion
  - localhost:9411 - zipkin traces
  - Create a `wavefront.env` file to configure against your api endpoint and api key

    ```
    WAVEFRONT_URL=https://{TENANT}.wavefront.com/api
    WAVEFRONT_TOKEN={API KEY}
    ```

**Other**

- `gitea` - Gitea - lightweight git server
  - http://localhost:3000