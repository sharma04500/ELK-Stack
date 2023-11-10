#   File Beat

Filebeat is a beat which has the potential to ingest the data from the log files of the system and ship it to the elasticsearch. 
*In elastic stack, a Beat is a lightweight data shipper which comes with action-specific capabilities.*
Beats are installed on the *application servers* and are directly configured to the elasticsearch or logstash. while integrating the beats with elaticsearch or logstash, accessibility is a mandatory check point.

![filebeat!](filebeat.png)

#### Installation
Beats can be installed from the elatic repository from which we've installed the elasticsearch and kibana. To install a file beat on any application server, first set up the elastic repository and update the apt lists using the following commands. If you're installing file beat on the server carrying elasticsearch and kibana, user can directly execute `apt install -y filebeat`, as the repository is already active and available.


```
# PGP key for the elastic repository:

wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo gpg --dearmor -o /usr/share/keyrings/elasticsearch-keyring.gpg

echo "deb [signed-by=/usr/share/keyrings/elasticsearch-keyring.gpg] https://artifacts.elastic.co/packages/8.x/apt stable main" | sudo tee /etc/apt/sources.list.d/elastic-8.x.list

apt update && apt install elasticsearch -y

```
