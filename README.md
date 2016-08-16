# Grab Elasticsearch 5 from https://www.elastic.co/downloads/elasticsearch
wget https://download.elastic.co/elasticsearch/release/org/elasticsearch/distribution/zip/elasticsearch/5.0.0-alpha5/elasticsearch-5.0.0-alpha5.zip

# Grab Kibana 5 from https://www.elastic.co/downloads/kibana
wget https://download.elastic.co/kibana/kibana/kibana-5.0.0-alpha5-darwin-x86_64.tar.gz

# Grab Filebeat 5 from https://www.elastic.co/downloads/beats/filebeat
wget https://download.elastic.co/beats/filebeat/filebeat-5.0.0-alpha5-darwin-x86_64.tar.gz

# Grab Packetbeat 5 from https://www.elastic.co/downloads/beats/packetbeat
wget https://download.elastic.co/beats/packetbeat/packetbeat-5.0.0-alpha5-darwin-x86_64.tar.gz

# Grab Metricbeat 5 from https://www.elastic.co/downloads/beats/metricbeat
wget https://download.elastic.co/beats/metricbeat/metricbeat-5.0.0-alpha5-darwin-x86_64.tar.gz

# Extract all archives
unzip elasticsearch-5.0.0-alpha5.zip

tar xzvf kibana-5.0.0-alpha5-darwin-x86_64.tar.gz
tar xzvf filebeat-5.0.0-alpha5-darwin-x86_64.tar.gz
tar xzvf metricbeat-5.0.0-alpha5-darwin-x86_64.tar.gz
tar xzvf packetbeat-5.0.0-alpha5-darwin-x86_64.tar.gz

# Install X-Pack (commercial, 30 day trial)
cd elasticsearch-5.0.0-alpha5
bin/elasticsearch-plugin install x-pack

cd ../kibana-5.0.0-alpha5-darwin-x86_64
bin/kibana-plugin install x-pack



