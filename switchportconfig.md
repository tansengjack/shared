[Main Menu](../README.md)
#PortConfiguration

## Switch port configuration

### Access Mode


```shell
ansible-playbook cisco_portconfig_sn.yml -i inventory -e \
'{
"config_type":"switch_port_configuration",
"operation":"create",
"abort_if_int_connected":"true",
"config":[
          {"name":"GigabitEthernet1/0/4","access":{"vlan":100},"description":"Configuring via ansible "}
         ]
}'
```


### Trunk Mode

```shell
ansible-playbook cisco_portconfig_sn.yml -i inventory -e \
'{
"config_type":"switch_port_configuration",
"operation":"create",
"abort_if_int_connected":"true",
"config":[
          {"name":"GigabitEthernet1/0/5","trunk":{"vlan_range":"60-70"},"description":"Configuring in trunk mode "}
         ]
}'

```
### Trunk Mode with curl command
```shell
export var='{"extra_vars" :
"{
\"config_type\":\"switch_port_configuration\",
\"operation\":\"create\",
\"config\":[
{\"name\":\"GigabitEthernet1/0/5\",\"trunk\":{"vlan_range":"60-70"},\"description\":\"Configuring in trunk mode\"},
{\"name\":\"GigabitEthernet1/0/6\",\"trunk\":{"vlan_range":"80-90"},\"description\":\"Configuring in trunk mode\"}
]
}"
}'
echo $var | curl -v -k -u admin:admin -H 'content-type: application/json' -X  POST -d "$(</dev/stdin)" https://172.16.240.138/api/v2/job_templates/474/launch/ 
```


### PortMapping

```shell
ansible-playbook cisco_portconfig_sn.yml -i inventory -e \
'{
"config_type":"switch_port_configuration",
"operation":"create",
"abort_if_int_connected":"true",
"config":[
          {"name":"GigabitEthernet1/0/8","port_mapping":{"vlan_num":22,port_channel_num: 2},"description":"Configuring port mapping "}
         ]
}'
```
### PortMapping with curl command
```shell
export var='{"extra_vars" :
"{
\"config_type\":\"switch_port_configuration\",
\"operation\":\"create\",
\"config\":[
{\"name\":\"GigabitEthernet1/0/8\",\"port_mapping\":{\"vlan_num\":22,port_channel_num: 2},\"description\":\"Configuring port mapping \"},
{\"name\":\"GigabitEthernet1/0/9\",\"port_mapping\":{\"vlan_num\":23,port_channel_num: 2},\"description\":\"Configuring port mapping \"}
]
}"
}'
echo $var | curl -v -k -u admin:admin -H 'content-type: application/json' -X  POST -d "$(</dev/stdin)" https://172.16.240.138/api/v2/job_templates/474/launch/ 
```



### Layer2 (VLAN)

```shell
ansible-playbook cisco_portconfig_sn.yml -i inventory -e \
'{
"config_type":"vlan_configuration",
"operation":"create",
"abort_if_int_connected":"true",
"config":
         [
            {"name":"Vlan_100","vlan_id":100}
         ]
 }'
```
### Layer2 (VLAN) with curl command

```shell
export var='{"extra_vars" :
"{
\"config_type\":\"vlan_configuration\",
\"operation\":\"create\",
\"config\":[
{\"name\":\"Vlan_100\",\"vlan_id\":100},
{\"name\":\"Vlan_200\",\"vlan_id\":200}
]
}"
}'
echo $var | curl -v -k -u admin:admin -H 'content-type: application/json' -X  POST -d "$(</dev/stdin)" https://172.16.240.138/api/v2/job_templates/474/launch/ 
```


### Layer 3 (Logical)

```shell
ansible-playbook  cisco_portconfig_sn.yml -i inventory -e '{
"config_type":"LOGICAL_LAYER3",
"operation":"create",
"abort_if_int_connected":"true",
"config":[
            {
                "name":"Vlan_99",
                "vlan_id":99,
                "ipv4addr":"10.6.0.1",
                "ip_mask":"255.255.255.0",
                "ipv6addr":"2001:df3:bf80:4285:10:152:120:222/64",
                "description": "Creating via ansible"
                }
         ]
}'
```
### Layer 3 (Logical) with curl command
```shell
export var='{"extra_vars" :
"{
\"config_type\":\"LOGICAL_LAYER3\",
\"operation\":\"create\",
\"config\":[
{\"name\":\"Vlan_10\",\"vlan_id\":10,\"ipv4addr\":\"1.1.1.1\", \"ip_mask\":\"255.255.255.0\",\"ipv6addr\":\"2001:df6:bf85:4285:10:152:120:222/64\",\"description\": \"Creating via ansible\"},
{\"name\":\"Vlan_20\",\"vlan_id\":20,\"ipv4addr\":\"1.1.2.1\", \"ip_mask\":\"255.255.255.0\",\"ipv6addr\":\"2001:df5:bf86:4285:10:152:120:222/64\",\"description\": \"Creating via ansible\"}
]
}"
}'
echo $var | curl -v -k -u admin:admin -H 'content-type: application/json' -X  POST -d "$(</dev/stdin)" https://172.16.240.138/api/v2/job_templates/474/launch/ 
```



### Layer 3 (Physical)

```shell
ansible-playbook cisco_portconfig_sn.yml -i inventory -e '{
"config_type":"PHYSICAL_LAYER3",
"operation":"create",
"abort_if_int_connected":"true",
"config":[
            {
                "name":"GigabitEthernet1/0/10",
                "ipv4addr":"10.6.0.1",
                "ip_mask":"255.255.255.0",
                "description": "Creating via ansible"
                }
         ]
}'
```
### Layer 3 (Physical) with curl command
```shell
export var='{"extra_vars" :
"{
\"config_type\":\"PHYSICAL_LAYER3\",
\"operation\":\"create\",
\"config\":[
{\"name\":\"GigabitEthernet1/0/10\",\"ipv4addr\":\"11.1.0.1\",\"ip_mask\":\"255.255.255.0\",\"description\": \"Creating via ansible\"},
{\"name\":\"GigabitEthernet1/0/11\",\"ipv4addr\":\"12.1.0.1\",\"ip_mask\":\"255.255.255.0\",\"description\": \"Creating via ansible\"}
]
}"
}'
echo $var | curl -v -k -u admin:admin -H 'content-type: application/json' -X  POST -d "$(</dev/stdin)" https://172.16.240.138/api/v2/job_templates/474/launch/ 
```
