#   Kibana

Kibana is a powerful visualization tool, which is designed and developed by the 'elastic' company. Kibana is another major component of the elastic stack or the elk stack. which visualises the data stored in the elasticsearch.

#### Installation of *kibana*:

Kibana can be installed from the official repository of the elastic company. So, To install kibana, we have to setup the elastic repository. If you've installed elasticsearch on the same node on which you're installing kibana, you can directly execute `apt install -y kibana` as you would've already setup the repository for the elasticsearch. To setup the repo, follow the below commands;
```
# PGP key for the elastic repository:

wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo gpg --dearmor -o /usr/share/keyrings/elasticsearch-keyring.gpg

echo "deb [signed-by=/usr/share/keyrings/elasticsearch-keyring.gpg] https://artifacts.elastic.co/packages/8.x/apt stable main" | sudo tee /etc/apt/sources.list.d/elastic-8.x.list

apt update && apt install kibana -y

```

