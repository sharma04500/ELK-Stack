#   File Beat

Filebeat is a beat which has the potential to ingest the data from the log files of the system and ship it to the elasticsearch. 
*In elastic stack, a Beat is a lightweight data shipper which comes with action-specific capabilities.*
Beats are installed on the *application servers* and are directly configured to the elasticsearch or logstash. while integrating the beats with elaticsearch or logstash, accessibility is a mandatory check point.



![filebeat!]("./filebeat.png")

#### Installation
Beats can be installed from the elatic repository from which we've installed the elasticsearch and kibana. Usually, to install a file beat on any application server, first set up the repository for the 