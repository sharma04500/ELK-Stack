# ELASTICSEARCH

Elastic search is an open-source NoSQL Database from the elastic company. Elastic search is the heart of the elastic stack, as it stores the entire information in the form of JSON doccuments. 

Beats or Logstash will feed the data into elasticsearch. Kibana will pull the data from the elasticsearch and visualizes it for provisioning ease to read it through customized and predifined views.

### Installing ElasticSearch:

Elasticsearch was purely built on Java and comes with the required java modules bundled along with the downloaded elasticsearch installation package. We need not to install java for using elasticsearch.

To install elasticsearch, first setup the repository of elastic with the aid of the PGP key and add this repository definition to the apt sources list through executing the following commands:

```
# PGP key for the elastic repository:

wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo gpg --dearmor -o /usr/share/keyrings/elasticsearch-keyring.gpg

echo "deb [signed-by=/usr/share/keyrings/elasticsearch-keyring.gpg] https://artifacts.elastic.co/packages/8.x/apt stable main" | sudo tee /etc/apt/sources.list.d/elastic-8.x.list

apt update && apt install elasticsearch -y

```

Logstash, Kibana and beats can also be installed from the same repository as elastic updates their latest release information through this official repository.

After installing the elasticsearch, go through the elasticsearch configuration file and make necessary modifications in order to configure the elastic search for provisioning appropriate accessibility to the kibana and logstash or beats.

The path for the elasticsearch configuration file is `/etc/elasticsearch/elasticsearch.yml`

#### Modification of listen address

By default, elasticsearch will be listening only on 9200 port of localhost, i.e., the applications installed on the same VM only can access the elasticsearch. In this case, both Kibana and beats should also be with in the same VM. In order to provision the accessibility to to the other elastic components or shards or replicas of the elasticsearch, we have to change this parameter, as per our requirements in the configuration file.

Open the elasticsearch.yml file and make changes in the *--NETWORK--* section.

Change `network.host: "localhost"` to `network.host: 0.0.0.0`.
*This modification lets elasticsearch to be accessible for any incomming connections.* i.e., `ipaddress:9200` in browser takes you to the elasticsearch.

Instead of doing this, we can also specify IP addresses of the machines, which intend to contact the Elasticsearch.

#### Modification of discovery section for cluster formation

Seed host discovery refers to an auto-clustering mechanism in Elasticsearch. While setting up an elasticsearch cluster, if we describe all the nodes which belong to the cluster in this section through mentioning the ip address or an ip address with port or a domain name whose endpoint is another node carrying elaticsearch, as shown below. Elasticsearch has the capability to automatically spin up a cluster using the provided hosts and auto elects the master node as well.

The other nodes on which elasticsearch is running are specified as seed hosts under discovery section. Here, the hosts can be specified as values in yaml format directly or as a list of strings, as shown below:

```
discovery.seed_hosts:
   - 192.168.1.10:9300
   - 192.168.1.11
   - seeds.mydomain.com

# or like list of Strings :
discovery.seed_hosts: ["192.168.1.10:9300", "192.168.1.11", "seeds.mydomain.com"]

```

#### Using Environment Variables

Elasticsearch.yml file supports usage of environment variables and to call them in the file just use ${}. <br>
For example to specify the node name, we can set an env using `export HOST="172.25.16.30,172.25.16.32"`. This will set an environment variable HOST with the value "172.25.16.30,172.25.16.32". The config file reads this value as two different IP addresses and will process the variable two times for the two IP addresses specified using comma(,).

To call the environment variable in the file, mention it as `${HOST}`. 

For example: 
```
node.name: ${HOSTNAME}
```
#### Shards and Replicas

Like anyother Databases available in the market, ElasticSearch also supports the concept of Shards and Replicas. The fundamental difference between the shards and replicas is shards are the partitions of the entire Database and Replica is a cloned copy of the entire DB.

> Shards
>> In case of Shards, the entire Database is divided into multiple parts and each shard will hold a partition of the data. In case of RDB's, Shards usually hold few columns of the entire DB. Sharding lets the elasticsearch to process the queries much faster when compared to a standalone Database. If any of the shards go down, the queries being processed will be affected and the outputs contain partial data, due to unavailability of a part of the database.

> Replicas
>> In case of Replicas, each replica holds the copy of the entire Database. The incomming queries will shared among the replicas and master node for processing. If a replica goes down, the query processing will slow down. But, the data which is being provided will be complete.

Though the concept of Replicas and shards is unique, the purpose of both is same i.e., to enable the elasticsearch to process the queries.






Reference: https://www.elastic.co/guide/en/elasticsearch/reference/current/deb.html