# stagemonitor docker-compose

This docker-compose file consists of Elasticsearch and Kibana with the [stagemonitor Kibana plugin](https://github.com/stagemonitor/stagemonitor-kibana).

### Install Docker AND Docker Compose
```
wget -qO- https://get.docker.com/ | sh
# add current user to focker group
sudo usermod -aG docker $(whoami)
sudo apt-get -y install python-pip
sudo pip install docker-compose
```
### Fetch configuration AND run it
```
git clone https://github.com/littleserg/stagemonitor-docker-compose.git
cd stagemonitor-docker-compose
docker-compose build
docker-compose up
```

### Add to startup script
```
crontab -e
# add there
@reboot docker-compose -f /<PATH>/stagemonitor-docker-compose/docker-compose.yml start
```

To start the containers in the background run `docker-compose up -d`.

It can take several minutes to build the image. Especially, the build step `Optimizing and caching browser bundles...`.
If you want to get started quicker, comment out the build line and uncomment the image line.


Also, the first startup of Kibana can take a while. Don't give up when you see this message: 
```
Optimizing and caching bundles for stagemonitor-kibana, kibana, stateSessionStorageRedirect, timelion and status_page. This may take a few minutes
```

A few minutes later, you'll see this log message which indicates Kibana is now ready to be accessed.

```
Optimization of bundles for stagemonitor-kibana, kibana, stateSessionStorageRedirect, timelion and status_page complete in 163.71 seconds
```

## Elasticsearch

| Type of Elasticsearch installation    | Elasticsearch URL         |
|---------------------------------------|---------------------------|
| docker-compose on local linux machine or docker for mac/windows | [http://localhost:9200](http://localhost:9200) |
| docker-compose with docker toolbox    | http://192.168.99.100:9200 *|

`*` The IP can vary. Execute `docker-machine ip default` to see the actual IP if the default one doesn't work

## Kibana
| Type of Kibana installation           | Kibana URL                |
|---------------------------------------|---------------------------|
| docker-compose on local linux machine or docker for mac/windows | [http://localhost:5601](http://localhost:5601) |
| docker-compose with docker toolbox    | http://192.168.99.100:5601 *|

`*` The IP may vary. Execute `docker-machine ip default` to see the actual IP if the default one doesn't work