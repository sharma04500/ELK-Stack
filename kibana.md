#   Kibana

Kibana is a powerful visualization tool, which is designed and developed by the 'elastic' company. Kibana is another major component of the elastic stack or the elk stack. which visualises the data stored in the elasticsearch.

#### Installation of *kibana*:

Kibana is developed on Javascript and Typescript. Kibana can be installed from the official repository of the elastic company. So, To install kibana, we have to setup the elastic repository. If you've installed elasticsearch on the same node on which you're installing kibana, you can directly execute `apt install -y kibana` as you would've already setup the repository for the elasticsearch. To setup the repo, follow the below commands:
```
# PGP key for the elastic repository:

wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo gpg --dearmor -o /usr/share/keyrings/elasticsearch-keyring.gpg

echo "deb [signed-by=/usr/share/keyrings/elasticsearch-keyring.gpg] https://artifacts.elastic.co/packages/8.x/apt stable main" | sudo tee /etc/apt/sources.list.d/elastic-8.x.list

apt update && apt install kibana -y

```
On installation, Kibana will neither start nor be enabled by default. But the installer package automatically creates a systemd module for the application.

The kibana configuration file will be in the path: `/etc/kibana/kibana.yml`
Before starting or enabling kibana, we have to set up the necessary configuration for the kibana dashboard for provisioning accessibility and security to kibana. 

#### Listen Addresses
By default, Kibana will be configured to connect to the elasticsearch on the 9200 port of the localhost i.e., kibana by default tries to access elasticsearch on https://localhost:9200 

Similarly Kibana dashboard will be accessible only on the localhost via 5601 as per the default config file i.e., kibana dashboard can be accessible only via http://localhost:5601. We have to change this configuration to 0.0.0.0 or our IP address, in order to access the kibana dashboard from our systems.

To modify the above said fields, open the configuration file using vi editor: `vi /etc/kibana/kibana.yml`

To change the listen address of the kibana dashboard, change the `server.host: "localhost"` field to `server.host: "0.0.0.0"` or for additional privacy, set `server.host: "172.25.16.53"`, if your system IP address is 172.25.16.53 under system: kibana server section of the config file.

If elasticsearch is sitting on a different VM, also modify the `elasticsearch.hosts: ["http://localhost:9200"]` to `elaticsearch.hosts: ["http://<elasticsearch_IP>:9200"]` also change the port, if the port number is modified in the elasticsearch.

In case of using a customized port for any of the applications like elasticsearch or kibana, Make sure that the port mentioned in the URL is reachable and accurate.

#### Configure the stack after installation

To login into the kibana dashboard, The stack will create `kibana_system` user by default for logging in to the dashboard initially.
The credentials for this user can be found at the bottom most lines of the kibana configuration file in the columns as shown:
```
elasticsearch.username: kibana_system
elasticsearch.password: m=kvZCyod*JtaJYvPK9Y
```
**NOTE:** *These credentials are unique for every installation.*

Once, after starting elasticsearch and kibana using systemctl, access the IP of the instance via 5601 port via browser to configure Kibana.
`http://localhost:5601`

To generate an enrollment token for kibana, execute the following command in the CLI:
```
/usr/share/elasticsearch/bin/elasticsearch-create-enrollment-token -s kibana
```
Now, the dashboard will prompt for the kibana verification code, which you can get through executing the following command in the Kibana instance *(for linux machines only)* or `systemctl status kibana` also pops up the verification code to be entered in the dashboard for configuring the dashboard with server.

```
/usr/share/kibana/bin/kibana-verification-code
```