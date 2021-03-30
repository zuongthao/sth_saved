
Ref: 

https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-elasticsearch-on-ubuntu-16-04

https://devdocs.magento.com/guides/v2.4/config-guide/elasticsearch/configure-magento.html

#### Download ElasticSearch
   https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.6.0-amd64.deb
or
https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.12.0-amd64.deb

#### Install ElasticSearch
```
sudo dpkg -i elasticsearch-7.6.0-amd64.deb
```

```
sudo gedit /etc/elasticsearch/elasticsearch.yml
```
then change as below:
```
cluster.name: magnus-el-search
node.name: "Magnus First Node"
```

#### Start ElasticSearch
```
sudo service elasticsearch start
```

#### Testing ElasticSearch
go to http://localhost:9200 and see the JSON response

#### Integration ElasticSearch & Magento 2
Edit file Nginx configuration of Magento site then add as 
```
location /_cluster/health {
    proxy_pass http://localhost:9200/_cluster/health;
}
```
Make sure app/etc/config.php has
```
'Magento_Elasticsearch' => 1,
'Magento_Elasticsearch7' => 1,
```
- Log in to the Magento Admin as an administrator.
- Click Stores > Settings > Configuration > Catalog > Catalog > Catalog Search.
- From the Search Engine list, select your Elasticsearch version.