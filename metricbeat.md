#  Metric Beat
Metric beat is used to push the resource metrics of the application server into the elaticsearch. 

In short, what metric beat does is, it collects the specified metric data and pushes it into the elasticsearch and Kibana visualizes the data from the elasticsearch.

```
# PGP key for the elastic repository:

wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo gpg --dearmor -o /usr/share/keyrings/elasticsearch-keyring.gpg

echo "deb [signed-by=/usr/share/keyrings/elasticsearch-keyring.gpg] https://artifacts.elastic.co/packages/8.x/apt stable main" | sudo tee /etc/apt/sources.list.d/elastic-8.x.list

apt update && apt install filebeat -y

```
By default, the metric beat will be in stopped status on installation, but the package manager will auto create a systemd module for the metric beat.

Before manually starting the metric beat, we should properly configure it in order to establish the communication in between beat and elaticsearch or logstash.

The configuration file lies in the path: `/etc/metricbeat/metricbeat.yml` 