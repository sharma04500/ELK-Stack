# ELASTICSEARCH

Elastic search is an open-source NoSQL Database from the elastic company. Elastic search is the heart of the elastic stack, as it stores the entire information in the form of JSON doccuments. 

Beats or Logstash will feed the data into elasticsearch. Kibana will pull the data from the elasticsearch and visualizes it for provisioning ease to read it through customized and predifined views.

### Installing ElasticSearch:

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

The other nodes on which elasticsearch is running are specified as seed hosts under discovery section. Here, the hosts can be specified as values in yaml format directly or as a list of strings, as shown below:

```
discovery.seed_hosts:
   - 192.168.1.10:9300
   - 192.168.1.11
   - seeds.mydomain.com

# or

discovery.seed_hosts: ["192.168.1.10:9300", "192.168.1.11", "seeds.mydomain.com"]

```










Reference: https://www.elastic.co/guide/en/elasticsearch/reference/current/deb.html