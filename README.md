# Download
### Grab Elasticsearch 5 from https://www.elastic.co/downloads/elasticsearch
    wget https://download.elastic.co/elasticsearch/release/org/elasticsearch/distribution/zip/elasticsearch/5.0.0-alpha5/elasticsearch-5.0.0-alpha5.zip

### Grab Kibana 5 from https://www.elastic.co/downloads/kibana
    wget https://download.elastic.co/kibana/kibana/kibana-5.0.0-alpha5-darwin-x86_64.tar.gz

### Grab Packetbeat 5 from https://www.elastic.co/downloads/beats/packetbeat
    wget https://download.elastic.co/beats/packetbeat/packetbeat-5.0.0-alpha5-darwin-x86_64.tar.gz
    
On non-Mac platforms libpcap has to be installed before. Instructions here: https://www.elastic.co/guide/en/beats/packetbeat/current/packetbeat-installation.html 

### Grab Metricbeat 5 from https://www.elastic.co/downloads/beats/metricbeat
    wget https://download.elastic.co/beats/metricbeat/metricbeat-5.0.0-alpha5-darwin-x86_64.tar.gz

### Extract all archives
    unzip elasticsearch-5.0.0-alpha5.zip

    tar xzvf kibana-5.0.0-alpha5-darwin-x86_64.tar.gz
    tar xzvf metricbeat-5.0.0-alpha5-darwin-x86_64.tar.gz
    tar xzvf packetbeat-5.0.0-alpha5-darwin-x86_64.tar.gz

# Install
### X-Pack (commercial, 30 day trial)
    elasticsearch-5.0.0-alpha5/bin/elasticsearch-plugin install x-pack

    kibana-5.0.0-alpha5-darwin-x86_64/bin/kibana-plugin install x-pack
    
### Timelion
    kibana-5.0.0-alpha5-darwin-x86_64/bin/kibana-plugin install timelion
    
# Run
### Start Elasticsearch
A problem with the new Netty4 module in alpha5 requires switching back to Netty3 for the Import dashboards step further down to work.

    elasticsearch-5.0.0-alpha5/bin/elasticsearch -Ehttp.type=security3
    
### Start Kibana
    kibana-5.0.0-alpha5-darwin-x86_64/bin/kibana
    
### Start the Beats
`packetbeat.full.yml` and `metricbeat.full.yml` are from this repository.

    sudo packetbeat-5.0.0-alpha5-darwin-x86_64/packetbeat -e -c packetbeat.full.yml  -d "publish"
    sudo metricbeat-5.0.0-alpha5-darwin-x86_64/metricbeat -e -c metricbeat.full.yml - d "publish"
    
# Load dashboards
`cd` is necessary.
    
    cd packetbeat-5.0.0-alpha5-darwin-x86_64/kibana
    ./import_dashboards.sh -u elastic:changeme
    cd -
    
    cd metricbeat-5.0.0-alpha5-darwin-x86_64/kibana
    ./import_dashboards.sh -u elastic:changeme
    cd -
    
# View dashboards in Kibana
Go to http://localhost:5601/, log in with `elastic / changeme` (yes, you should change it ;-)).

Select one of the existing index patterns as the defauls: `packetbeat-*` and `metricbeat-*` should be listed in top left corner, select one and then click the star icon.

Go to Dashboards (left-hand navigation), click Open (top right) and select any.



