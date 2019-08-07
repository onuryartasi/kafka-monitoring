### INSTALL KAFKA

```
wget http://www-eu.apache.org/dist/kafka/1.1.0/kafka_2.11-1.1.0.tgz -P /tmp/
sudo tar -zxvf /tmp/kafka_2.11–1.1.0.tgz -C /opt/
sudo ln -s /opt/kafka_2.11–1.1.0 /opt/kafka
cp ./kafka-run-class.sh /opt/kafka/bin/
```

### INSTALL JMX EXPORTER

    git clone https://github.com/onuryartasi/kafka-monitoring
    cd kafka-monitoring
    cp -r ./prometheus /opt/kafka/
    
### ad args kafka-server-start.sh 
#prometheus jvm
EXTRA_ARGS="-javaagent:/opt/kafka/prometheus/jmx_prometheus_javaagent-0.9.jar=7071:/opt/kafka/prometheus/kafka-2_0_0.yml"
EXTRA_ARGS=${EXTRA_ARGS-'-name kafkaServer -loggc'}


### INSTALL PROMETHEUS

#### Create Prometheus Directory
    sudo mkdir /etc/prometheus /var/lib/prometheus /var/log/prometheus /var/run/prometheus

#### Install Prometheus
    wget https://github.com/prometheus/prometheus/releases/download/v2.10.0/prometheus-2.10.0.linux-amd64.tar.gz -P /tmp/

    sudo tar -zxvf /tmp/prometheus-2.10.0.linux-amd64.tar.gz -C /tmp/

    sudo cp /tmp/prometheus-2.10.0.linux-amd64/{prometheus,promtool} /usr/local/bin/

    sudo chmod +x /usr/local/bin/{prometheus,promtool}

     sudo cp /tmp/prometheus-2.10.0.linux-amd64/prometheus.yml /etc/prometheus/

     sudo cp -r /tmp/prometheus-2.10.0.linux-amd64/{consoles,console_libraries} /etc/prometheus/

#### Copy prometheus.yml to /etc/prometheus

    cp ./prometheus.yml /etc/prometheus/

#### Copy prometheus.service to /etc/systemd/system

    cp ./prometheus.service /etc/systemd/system/

#### And start prometheus

    sudo systemctl enable prometheus.service && sudo systemctl start prometheus
