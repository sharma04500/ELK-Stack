#  Elastic Stack

    Before knowing about elastic stack, we should know about ELK stack and how elk stack became elastic stack.

    ELK stack represents three products of 'elastic', which are generally used in combination for monitoring the 
performance of the VM's and containers. The three components of the ELK stack have their own significance as  
mentioned below.

E - Elasticsearch   ***Database***
L - LogStash        ***Collects Data***
K - Kibana          ***Visualises the data***

## Elastic Search
    Elastic search is the heart of the ELK, which stores all the data in NOSQL format. It uses json doccuments to
store the data in it. Elastic Search is basically a NoSQL type DB developed by elastic in order to fulfill the DB
requirements of the ELK stack. The largest possible data unit in ElasticSearch is Index i.e., the database in any
other platform like mongoDB or mysql in elastic search is referred as index in ElasticSearch.
    Like anyother databases, Elastic search also supports sharding and replica concepts to ensure high availability
of the stack at anytime.

## Logstash
    Logstash is simply a data collector. we should install Logstash on the server, from which we intend to monitor. 
As an application, logstash is heavy in nature and consumes a lot of resources on the server in which we are installing
logstash. Logstash has the ability to ship any kind of data like logs, metrics, files etc to elastic search. Logstash
pulls the structured or unstructured data from the server ans ships it to the ElasticSearch, which stores all this 
data.

## Kibana
    Kibana is a powerful visualization tool, which visualizes the data stored in elastic search and represents it
in an easily understandable graphical forms like pie charts, histograms etc. Kibana pulls the data from the elastic
search using respective queries, which displays it through a dashboard.

> #### Why Beats??
    During the initial years of introducing ELK stack to the market, Most of the users found logstash heavy and resource 
consuming. So, the company then introduced the concept of Beats. Beats are the fourth component added to the ELK stack.

## Beats
    Beats are the light weight data shippers which pulls resource-specific data and ships it to the logstash or directly 
to the elastic search. In case of beats, instead of packing all the abilities to pull various types of data from a server
like metrics, logs, uptime, files etc., into a single application (logstash), people developed individual small sized
entities with purpose-specific capabilities which can be installed anywhere. There are various types of beats. 
Types of Beats available are:
    1. **File Beat**
         - *File Beat* comes with the capability to capture the files and logs from the server and ship the files directly
         to elasticsearch *or to any other destintions like logstash or apache kafka as well*  
    2. **Metric Beat**
         - *Metric Beat* is another lightweight datashipper with the ability to collect the metrics data from the source
         and ship it to the destination (elastic search in general)
    3. **Packet Beat**
         - *Packet Beat* monitors the network flow and ships the networking data to the destination.
    4. **Winlog Beat**
         - *Winlog Beat* ingests the data logs, audit or any custom defined logs from the user's dashboard and ships it
         to the destination effortlessly. It is specifically designed for windows environments.
    5. **Audit Beat**
         - *Audit Beat* collects the audit data from the server and ships it to the destination. Audit data means the security
         logs like access logs, authentication logs, process execution logs etc and sends it to the destination.
    6. **Heart Beat**
         - *Heart Beat* ingests the server accessibility data and ships it to the elastic search in real-time. It continously 
        runs checks over http, https and icmp protocols and reports the availability.
    7. **Function Beat**
         - *Function Beat* ingests the cloud application data and sends it to the elastic search. In general, Function Beat is
         deployed as a serverless function in cloud and the beat collects all the data like cloudwatch logs and ships it to the
         elasticsearch.

## APM using ELK
    APM stands for Application Performance Monitoring.