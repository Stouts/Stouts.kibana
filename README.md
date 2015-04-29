Stouts.kibana
==============

[![Build Status](http://img.shields.io/travis/Stouts/Stouts.kibana.svg?style=flat-square)](https://travis-ci.org/Stouts/Stouts.kibana)
[![Galaxy](http://img.shields.io/badge/galaxy-Stouts.kibana-blue.svg?style=flat-square)](https://galaxy.ansible.com/list#/roles/1986)

Ansible role which manage [Kibana](http://www.elasticsearch.org/overview/kibana/)

* Install and configure kibana server

#### Dependencies

The roles are recomended to install:

* [Stouts.elasticsearch](https://github.com/Stouts/Stouts.elasticsearch) - for using as DB

#### Variables

Here is the list of all variables and their default values:

```yaml
kibana_enabled: yes                        # The role is enabled
kibana_version: 4.0.2                      # Set version
kibana_os_version: linux-x64
kibana_url: https://download.elastic.co/kibana/kibana/kibana-{{kibana_version}}-{{kibana_os_version}}.tar.gz

kibana_home: /var/www/kibana
kibana_user: www-data
kibana_group: "{{kibana_user}}"

# Kibana is served by a back end server
kibana_port: 5601
kibana_host: 0.0.0.0

# The Elasticsearch instance to use for all your queries.
kibana_elasticsearch_url: http://{{inventory_hostname}}:9200

# preserve_elasticsearch_host true will send the hostname specified in `elasticsearch`. If you set it to false,
# then the host you use to connect to *this* Kibana instance will be sent.
kibana_elasticsearch_preserve_host: true

# Kibana uses an index in Elasticsearch to store saved searches, visualizations
# and dashboards. It will create a new index if it doesn't already exist.
kibana_index: .kibana

# If your Elasticsearch is protected with basic auth, this is the user credentials
# used by the Kibana server to perform maintence on the kibana_index at statup. Your Kibana
# users will still need to authenticate with Elasticsearch (which is proxied thorugh
# the Kibana server)
kibana_elasticsearch_username:
kibana_elasticsearch_password:

# If your Elasticsearch requires client certificate and key
kibana_elasticsearch_client_crt:
kibana_elasticsearch_client_key:

# If you need to provide a CA certificate for your Elasticsarech instance, put
# the path of the pem file here.
kibana_ca:

# The default application to load.
kibana_default_app_id: discover

# Time in milliseconds to wait for responses from the back end or elasticsearch.
# This must be > 0
kibana_request_timeout: 300000

# Time in milliseconds for Elasticsearch to wait for responses from shards.
# Set to 0 to disable.
kibana_shard_timeout: 0

# Set to false to have a complete disregard for the validity of the SSL
# certificate.
kibana_verify_ssl: true

# SSL for outgoing requests from the Kibana Server (PEM formatted)
kibana_ssl_key_file:
kibana_ssl_cert_file:

# Set the path to where you would like the process id file to be created.
kibana_pid_file: /var/run/kibana.pid

# Plugins that are included in the build, and no longer found in the plugins/ folder
kibana_bundled_plugin_ids:
 - plugins/dashboard/index
 - plugins/discover/index
 - plugins/doc/index
 - plugins/kibana/index
 - plugins/markdown_vis/index
 - plugins/metric_vis/index
 - plugins/settings/index
 - plugins/table_vis/index
 - plugins/vis_types/index
 - plugins/visualize/index
```

#### Usage

Add `Stouts.kibana` to your roles and setup the variables in your playbook file.
Example:

```yaml

- hosts: all

  roles:
    - Stouts.elasticsearch
    - Stouts.kibana
```

#### License

Licensed under the MIT License. See the LICENSE file for details.

#### Feedback, bug-reports, requests, ...

Are [welcome](https://github.com/Stouts/Stouts.kibana/issues)!
