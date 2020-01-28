# zabbix-rabbitmq-plugin
Zabbix plugin for monitoring RabbmitMQ

## Installation

This plugin can be setup and run from the Zabbix server or on the RabbitMQ server itself.


### 1. Download the source to your Zabbix scripts path

**Example path: /etc/zabbix/scripts**

```
mkdir -p /etc/zabbix/scripts
cd /etc/zabbix/scripts
git clone https://github.com/eldarsudden/zabbix-rabbitmq-plugin.git
```

### 2. Setup Zabbix Agent

##### Make symlink to the zabbix-rabbitmq.conf into the "zabbix_agentd.d" directory
```
ln -s /etc/zabbix/scripts/zabbix-rabbitmq-plugin/zabbix_agentd.d/zabbix-rabbitmq.conf /etc/zabbix/zabbix_agentd.d/zabbix-rabbitmq.conf
```

### 3. Restart Zabbix Agent

```
systemctl restart zabbix-agent
```

### 4. Configuration

The `config.yml` contains RabbitMQ server settings.

### 5. Import the template

The `zabbix-rabbitmq-template.xml` file contains some basic discovery items, triggers and graphs. The template can be imported by going to the ***"Configuration/Templates"*** page in the Zabbix web console and by clicking the ***"import"*** button. 

## Invoke examples

Messages count for *ASYNC_DELAYED_QUEUE* queue:
```
 zabbix_get -s localhost -p 10050  -k 'rabbitmq.check.queue[localhost,/,ASYNC_DELAYED_QUEUE,messages]'
```
Discovery of cluster nodes:
```
zabbix_get -s localhost -p 10050  -k 'rabbitmq.discover.nodes["localhost"]'
```

## Db schema
```
CREATE TABLE CACHE(
   ID               INTEGER      PRIMARY KEY,
   HOSTNAME         CHAR(50)     NOT NULL,
   METHOD           CHAR(50)     NOT NULL,
   DATA             TEXT, 
   TIMESTAMP        INT          NOT NULL,
   VHOST            TEXT 
);
```
