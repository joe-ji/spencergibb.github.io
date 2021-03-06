## Spring Cloud <i class="fa fa-asterisk"></i>
### Alternative implementations of
### Discovery, Config & Bus

<style>img[alt=spring-cloud] { width: 40%; float: right; border: 0px solid #fff;}</style>

![spring-cloud](/images/spring-cloud.png)

Spencer Gibb<br>
<i class="fa fa-twitter"></i> [@spencerbgibb](http://twitter.com/spencerbgibb)<br>
<i class="fa fa-download"></i> [spencer.gibb.us/preso](http://spencer.gibb.us/preso)<br>
<i class="fa fa-envelope-o"></i> sgibb@pivotal.io



<!-- .slide: data-background="#FFFFFF" data-background-transition="zoom" -->
## ![pivotal](/images/pivotal_logo.png)

<style>img[alt=spring_io] { width: 40%; }</style>
<style>img[alt=gemfire] { width: 80%; }</style>
<style>img[alt=greenplum] { width: 40%; }</style>
<style>img[alt=tomcat] { width: 40%; }</style>

|               |               |       |
| ------------- |:-------------:| -----:|
| ![cf_logo](/images/cf_logo.png) | ![spring_io](/images/spring-io.png) | ![rabbitmq](/images/rabbitmq.png) |
| ![gemfire](/images/gemfire.png)  | ![greenplum](/images/greenplum.jpg) | ![pivotal_labs](/images/pivotal_labs_logo.png) |
| ![redis](/images/redis.png) | ![tomcat](/images/tomcat_logo.png) | ![bigtop](/images/bigtop.png) |



## Spring Cloud Components

* Service Discovery and Registration
* Distributed Configuration
* Control Bus
* Cluster primitives (Leader election, locks)



## Spring Cloud: Angel

* Netflix Eureka
* Spring Cloud Config
* Spring Cloud Bus AMQP (Rabbitmq)
* No Cluster Implementation



## Spring Cloud: Brixton

### Adds

* Hashicorp Consul
* Apache Zookeeper
* Sleuth (Tracing)
* Cluster
* CoreOS etcd (Incubator)



<!-- .slide: data-background="#B9090B" data-background-transition="zoom" -->
## Eureka
<style>img[alt=eureka] { float: right; width: 20%; }</style>
![eureka](/images/eureka.png)

* Netflix OSS
* Highly Available (prefers stale data vs<br>no data, AP in CAP)
* Long thresholds for registraion and<br>cache refresh (30s)
* Battle tested at Netflix



## Config Server and Client

* Greenfield
* HTTP API similar to Netflix Config Server
* Backed by VCS (git initially, then svn added)
* Stateless
* Uses spring-boot configuration files & semantics
* Auto-configured client



## Spring Cloud Bus AMQP

* Backed by Rabbitmq
* Distributed actuator
* Post messages via `/bus/*` actuator endpoints
* `/bus/refresh` and `/bus/env`



<!-- .slide: data-background="#294563" data-background-transition="zoom" -->
## Apache Zookeeper

<style>img[alt=zookeeper] { float: right; }</style>
![zookeeper](/images/zookeeper_small.gif)

* Consistent Distributed Coordination<br>server (CP in CAP)
* Started life as a Hadoop sub-project (2007?)
* Mature, used in many companies



### Spring Cloud Zookeeper Config

* Uses Apache Curator library
* Uses zookeeper to store hierarchical configuration
* Mimics Spring Cloud Config Server loading order
* Use a supervisory process like [Netflix Exhibitor](https://github.com/Netflix/exhibitor/wiki)



### Spring Cloud Zookeeper Discovery

* Uses Apache Curator Service Discovery Recipe
* Requires ephemeral nodes<br>
  (client must maintain active connection)
* Significant contribution from [4finance](https://github.com/4finance/micro-infra-spring)
* No Bus implementation

<blockquote>DEMO</blockquote> <!-- .element: class="fragment" -->



<!-- .slide: data-background="#694a9c" data-background-transition="zoom" -->
## Consul

* From Mitchell Hashimoto, creator of Vagrant
* Multi-datacenter aware
* peer-to-peer gossip system
* By default CP, but tunable
* Agent runs as a sidecar, connects to server cluster
* Web based UI



## Spring Cloud Consul Config

* Uses consul Key/Value (K/V) HTTP API to store hierarchical properties
* Mimics Spring Cloud Config Server loading order



### Spring Cloud Consul Discovery

* Full blown consul discovery service implementation
* HTTP API and DNS interface
* Rich health check system (HTTP, TCP or anything)



## Spring Cloud Consul Bus

* Uses Consul Event HTTP API
* Non-persistent control plane messages
* Uses Spring Integration



## Spring Cloud Consul

* Polyglot
* All-in-one (Discovery, config, bus, cluster)
 * `localhost:8500`
* Legacy support via DNS

<blockquote>DEMO</blockquote> <!-- .element: class="fragment" -->



<!-- .slide: data-background="#2276ad" data-background-transition="zoom" -->
## CoreOS Etcd

* <u>**Incubator Project**</u><br>(Not part of a release, yet)
* Distributed key/value store
* CP in CAP
* nice cli and HTTP API
* Many language bindings



## Spring Cloud Etcd Config

* Uses etcd Key/Value (K/V) HTTP API to store hierarchical properties
* Mimics Spring Cloud Config Server loading order



## Spring Cloud Etcd Discovery

* Bespoke implementation
 * creates value with TTL
* Uses HTTP API
* Spring `@Scheduled` heartbeat resets TTL

<blockquote>DEMO</blockquote> <!-- .element: class="fragment" -->



<!-- .slide: data-background="#2b6546" data-background-transition="zoom" -->
### Spring Cloud Lattice Discovery

* http://lattice.cf
* Single tenant cloudfoundry--
* Read Only
 * Lattice does registration
* Uses CF Diego Receptor API
* Connectors for: redis, mysql & rabbitmq



## Spring Cloud Cluster

* <u>**Brixton**</u>
* Distributed Locks
* Leader election



## Spring Cloud Cluster

* Hazelcast
* Redis
* *Zookeeper*
* Future: Consul<!-- .element: class="fragment" -->
* Future: Etcd<!-- .element: class="fragment" -->



## Questions<i class="fa fa-question"></i>

<i class="fa fa-twitter"></i> [@spencerbgibb](http://twitter.com/spencerbgibb)
<i class="fa fa-envelope-o"></i> [sgibb@pivotal.io](mailto:sgibb@pivotal.io)

<i class="fa fa-download"></i> [http://spencer.gibb.us/preso](http://spencer.gibb.us/preso/spring-cloud-star-springone-2015)

* <i class="fa fa-external-link"></i> [Simplicity Itself: Service Discovery Overview](http://www.simplicityitself.com/learning/getting-started-microservices/service-discovery-overview)
* <i class="fa fa-external-link"></i> [Knewton: Eureka vs Zookeeper](http://tech.knewton.com/blog/2014/12/eureka-shouldnt-use-zookeeper-service-discovery/)
* <i class="fa fa-external-link"></i> [Stackshare: Service Discovery Comparison](http://stackshare.io/stackups/consul-vs-zookeeper-vs-eureka)
* <i class="fa fa-external-link"></i> [Consul.io vs Zookeeper](https://www.consul.io/intro/vs/zookeeper.html)
* <i class="fa fa-external-link"></i> [Tech. Conversations: Zookeeper vs etcd vs Consul](http://technologyconversations.com/2015/09/08/service-discovery-zookeeper-vs-etcd-vs-consul/)
* <i class="fa fa-external-link"></i> https://zookeeper.apache.org
* <i class="fa fa-external-link"></i> https://coreos.com/etcd
