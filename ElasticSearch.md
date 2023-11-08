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

After installing the elasticsearch, go through the elasticsearch configuration file and make necessary modifications in order to configure the elastic search for provisioning appropriate accessibility to the kibana and logstash or beats.

The path for the elasticsearch configuration file is `/etc/elasticsearch/elasticsearch.yml`
