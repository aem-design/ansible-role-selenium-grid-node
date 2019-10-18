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
| grid_debug          	|          	| false                                                                                                                                                                                                                            	| grid debug mode                                                      	|
| grid_debug_vncport  	|          	| 5900                                                                                                                                                                                                                             	| vnc port for monitoring sessions if not headless                     	|
| grid_port           	|          	| 4444                                                                                                                                                                                                                             	| hub port                                                             	|
| grid_host           	|          	| localhost                                                                                                                                                                                                                        	| hub address                                                          	|
| grid_xvfb           	|          	| false                                                                                                                                                                                                                            	| run in headless mode                                                 	|
| grid_url                 	|          	| http://{{ grid_host }}:{{ grid_port }}                                                                                                                                                         	| hub url                                                              	|
| grid_status_node:  	|          	| /grid/api/proxy?id=                                                                                                                                                                                                               | status page for node                                               	|
| grid_status_schema  	|          	| http                                                                                                                                                                                                                             	| hub schema                                                           	|
| grid_status_url      |          	| {{ grid_status_schema }}://{{ grid_host }}:{{ grid_http_port }}{{ grid_status_service }} 	                                                                    | url for status                                                       	|
|                                      	|          	|                                                                                                                                                                                                                                  	|                                                                      	|
| docker_env                           	|          	|                                                                                                                                                                                                                                  	| environment variables                                                	|
| TZ                                   	|          	| {{ docker_timezone }}                                                                                                                                                                                                            	|                                                                      	|
| GRID_DEBUG                           	|          	| {{ grid_debug }}                                                                                                                                                                                                	|                                                                      	|
| HUB_HOST                             	|          	| {{ grid_host }}                                                                                                                                                                                                 	|                                                                      	|
| HUB_PORT                             	|          	| {{ grid_port }}                                                                                                                                                                                                 	|                                                                      	|
| START_XVFB                           	|          	| {{ grid_xvfb }}                                                                                                                                                                                                 	|                                                                      	|
| NODE_APPLICATION_NAME                	|          	| {{ docker_container_name }}                                                                                                                                                                                            	|                                                                      	|
|                                      	|          	|                                                                                                                                                                                                                                  	|                                                                      	|
| docker_published_ports                |          	| [                                                                                                                                                            	| default ports                                                        	|
|                                     	|          	| "0.0.0.0:{{ grid_http_port }}:4444/tcp",                                                                                                    	|                                                                      	|
|                                      	|          	| "0.0.0.0:{{ grid_debug_vncport }}:5900/tcp"                                                                                                 	|                                                                      	|
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
