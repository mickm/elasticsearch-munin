# Munin plugin for elasticsearch

A useful Munin plugin for monitoring elasticsearch 1.x nodes in Perl.<br />
This original codes has out of maintenance, so I have started maintenance this plugin.

## Plugins

* elasticsearch_cache - field and filter cache stats* elasticsearch_cluster_shards - cluster shards stats* elasticsearch_docs - document count* elasticsearch_index_size - index size* elasticsearch_index_total - index total count* elasticsearch_jvm_memory - JVM heap stats* elasticsearch_jvm_threads - JVM thread stats* elasticsearch_open_files - open files count* elasticsearch_translog_size - translog file size

## Configuration

### Variables

* env.host - a elasticsearch node capable of providing stats interface (default localhost)
* env.port - elasticsearch HTTP API port (default 9200)

### Example Config

Before use, put these settings into munin configuration.

  * examples of munin config file 
    *  in the case of all plugin config into single file.<br />
      `/etc/munin/plugin-conf.d/munin-node`
    * in the case of creating file per plugins.<br />
      `/etc/munin/plugin-conf.d/elasticsearch`

##### example of minimam configuration<br />

`elasticsearch_open_files` has required root privilege to read under the `/proc`.

```
[elasticsearch_open_files]
user root
```

##### example of custom host and port configuration

```
[elasticsearch_*]
env.host localhost
env.port 9200

[elasticsearch_open_files]
user root
env.host localhost
env.port 9200
```

## Install

Install this plugins with following steps after config setuped.

```sh
# For centos
$ cd /usr/local/src/
$ git clone https://github.com/y-ken/munin-plugin-elasticsearch.git
$ cd munin-plugin-elasticsearch
$ cp -p elasticsearch_* /usr/share/munin/plugins/
$ ln -s /usr/share/munin/plugins/elasticsearch_* /etc/munin/plugins/
$ sudo -H munin-node-configure --shell | grep elasticsearch | sudo -H sh
$ munin-node-configure | grep elasticsearch
$ service munin-node restart
```

To confirm wokring fine or not, you can check like below.

```sh
$ munin-run elasticsearch_jvm_memory
heap_init.value 8589934592
non_heap_max.value 224395264
heap_max.value 8520204288
direct_max.value 8520204288
non_heap_init.value 24313856
```

## Author

* Original code by [@rafl](https://github.com/rafl) has imported from https://gist.github.com/2159398
* [Contributors to y-ken/munin-plugin-elasticsearch](https://github.com/y-ken/munin-plugin-elasticsearch/graphs/contributors)
* maintained by [@y-ken](https://github.com/y-ken)

## Licence

MIT License
