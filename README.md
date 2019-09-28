# Ansible Role: Selenium Grid Node

[![Build Status](https://travis-ci.org/aem-design/ansible-role-selenium-grid-node.svg?branch=master)](https://travis-ci.org/aem-design/ansible-role-selenium-grid-node)

Setup Selenium Grid node for your Selenium Grid to test your services.
> This role was developed as part of
> [AEM.Design](http://aem.design/)

## Requirements

None.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

| Name                                 	| Required 	| Default                                                                                                                                                                                                                          	| Notes                                                                	|
|--------------------------------------	|----------	|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------	|----------------------------------------------------------------------	|
| docker_image_user                    	|          	| selenium                                                                                                                                                                                                                         	| docker user for image                                                	|
| docker_image_name                    	|          	| node-chrome                                                                                                                                                                                                                      	| docker image name                                                    	|
| docker_image                         	|          	| {{ docker_image_user }}/{{ docker_image_name }}                                                                                                                                                                                  	| full docker image                                                    	|
| docker_image_tag                     	|          	| latest                                                                                                                                                                                                                           	| docker image tag                                                     	|
| docker_container_name                	|          	| selenium-grid-{{ docker_image_name }}                                                                                                                                                                                            	| default container name                                               	|
| docker_timezone                      	|          	| Australia/Melbourne                                                                                                                                                                                                              	| timezone                                                             	|
| docker_shm_size                      	|          	| 1g                                                                                                                                                                                                                               	| ram to use for instance                                              	|
|                                      	|          	|                                                                                                                                                                                                                                  	|                                                                      	|
| service_selenium_grid_debug          	|          	| false                                                                                                                                                                                                                            	| grid debug mode                                                      	|
| service_selenium_grid_debug_vncport  	|          	| 5900                                                                                                                                                                                                                             	| vnc port for monitoring sessions if not headless                     	|
| service_selenium_grid_port           	|          	| 4444                                                                                                                                                                                                                             	| hub port                                                             	|
| service_selenium_grid_host           	|          	| localhost                                                                                                                                                                                                                        	| hub address                                                          	|
| service_selenium_grid_xvfb           	|          	| false                                                                                                                                                                                                                            	| run in headless mode                                                 	|
| service_selenium_url                 	|          	| http://{{ service_selenium_grid_host }}:{{ service_selenium_grid_port }}                                                                                                                                                         	| hub url                                                              	|
| service_selenium_grid_status_service 	|          	| /grid/console                                                                                                                                                                                                                    	| status page for hub                                                  	|
| service_selenium_grid_status_schema  	|          	| http                                                                                                                                                                                                                             	| hub schema                                                           	|
| service_selenium_grid_status_url      |          	| {{ service_selenium_grid_status_schema }}://{{ service_selenium_grid_host }}:{{ service_selenium_grid_http_port }}{{ service_selenium_grid_status_service }} 	                                                                    | url for status                                                       	|
|                                      	|          	|                                                                                                                                                                                                                                  	|                                                                      	|
| service_selenium_grid_status_test     |           | applicationName: {{ docker_container_name }}                                                                                                                                                                            | status test when hub has node added                                    |
|                                      	|          	|                                                                                                                                                                                                                                  	|                                                                      	|
| docker_env                           	|          	|                                                                                                                                                                                                                                  	| environment variables                                                	|
| TZ                                   	|          	| {{ docker_timezone }}                                                                                                                                                                                                            	|                                                                      	|
| GRID_DEBUG                           	|          	| {{ service_selenium_grid_debug }}                                                                                                                                                                                                	|                                                                      	|
| HUB_HOST                             	|          	| {{ service_selenium_grid_host }}                                                                                                                                                                                                 	|                                                                      	|
| HUB_PORT                             	|          	| {{ service_selenium_grid_port }}                                                                                                                                                                                                 	|                                                                      	|
| START_XVFB                           	|          	| {{ service_selenium_grid_xvfb }}                                                                                                                                                                                                 	|                                                                      	|
| NODE_APPLICATION_NAME                	|          	| {{ docker_container_name }}                                                                                                                                                                                            	|                                                                      	|
|                                      	|          	|                                                                                                                                                                                                                                  	|                                                                      	|
| docker_published_ports                |          	| [                                                                                                                                                            	| default ports                                                        	|
|                                     	|          	| "0.0.0.0:{{ service_selenium_grid_http_port }}:4444/tcp",                                                                                                    	|                                                                      	|
|                                      	|          	| "0.0.0.0:{{ service_selenium_grid_debug_vncport }}:5900/tcp"                                                                                                 	|                                                                      	|
|                                      	|          	| ]                                                                                                                                                            	|                                                                      	|
|                                      	|          	|                                                                                                                                                                                                                                  	|                                                                      	|
| docker_volumes                       	|          	|                                                                                                                                                                                                                                  	| default volumes                                                      	|
|                                      	|          	| "/dev/shm:/dev/shm"                                                                                                                                                                                                            	|                                                                      	|
|                                      	|          	| "/e2e/uploads:/e2e/uploads"                                                                                                                                                                                                    	|                                                                      	|
|                                      	|          	|                                                                                                                                                                                                                                  	|                                                                      	|
| wait_delay                           	|          	| 1                                                                                                                                                                                                                                	| how long to wait between retries                                     	|
| docker_host                          	|          	| unix://var/run/docker.sock                                                                                                                                                                                                       	| host where to run the docker container for executing pyaem2 commands 	|
|                                      	|          	|                                                                                                                                                                                                                                  	|                                                                      	|

## Dependencies

None.

## Example Playbook

```yaml
- hosts: all
  roles:
    - { role: aem_design.selenium_grid_node
    }
```

## License

Apache 2.0

## Author Information

This role was created by [Max Barrass](https://aem.design/).