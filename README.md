# Ansible Role: Selenium Grid Node

[![Build Status](https://travis-ci.org/aem-design/ansible-role-selenium-grid-node.svg?branch=master)](https://travis-ci.org/aem-design/ansible-role-selenium-grid-node)

Setup Selenium Grid node for your Selenium Grid to test your services.
> This role was developed as part of
> [AEM.Design](http://aem.design/)

## Requirements

None.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

| Name                            	| Required 	| Default                                                                               	| Notes                            	|
|---------------------------------	|----------	|---------------------------------------------------------------------------------------	|----------------------------------	|
| docker_image_user               	|          	| selenium                                                                              	|                                  	|
| docker_image_name               	|          	| node-chrome                                                                           	|                                  	|
| docker_image                    	|          	| {{ docker_image_user }}/{{ docker_image_name }}                                       	|                                  	|
| docker_image_tag                	|          	| latest                                                                                	|                                  	|
| docker_container_name           	|          	| selenium-grid-{{ docker_image_name }}-{{ ansible_date_time.iso8601_micro | to_uuid }} 	|                                  	|
| docker_timezone                 	|          	| Australia/Melbourne                                                                   	|                                  	|
|                                 	|          	|                                                                                       	|                                  	|
| service_selenium_grid_name      	|          	| selenium-grid                                                                         	|                                  	|
| service_selenium_grid_http_port 	|          	| 4444                                                                                  	|                                  	|
| service_selenium_grid_host      	|          	| localhost                                                                             	|                                  	|
|                                 	|          	|                                                                                       	|                                  	|
| docker_volumes                  	|          	|                                                                                       	|                                  	|
|                                 	|          	| - "/dev/shm:/dev/shm"                                                                 	|                                  	|
|                                 	|          	|                                                                                       	|                                  	|
| docker_links                    	|          	|                                                                                       	|                                  	|
|                                 	|          	| - "{{ service_selenium_grid_name | default('selenium-grid') }}:hub"                   	|                                  	|
|                                 	|          	|                                                                                       	|                                  	|
| iptable_rules                   	|          	|                                                                                       	|                                  	|
|                                 	|          	| - port: "{{ service_selenium_grid_http_port | default('4444') }}"                     	|                                  	|
|                                 	|          	| comment: "{{ docker_container_name }}"                                                	|                                  	|
|                                 	|          	|                                                                                       	|                                  	|
| wait_delay                      	|          	| 1                                                                                     	| how long to wait between retries 	|

## Dependencies

This role depends on roles:
 
- `aem_design.docker_container`

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