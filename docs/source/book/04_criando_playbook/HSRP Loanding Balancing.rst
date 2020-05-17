HSRP Loading Balancing
----------------------

Irá ser alocado o módulo ios_config nas duas tasks abaixo para criar dois grupos de HSRP seguidos de SVIs para fazer load balancing de tráfego entre as vlans.

Configurando SVIs e HSRP load balancing no SW_CORE_1:

.. code:: yaml

    #Configuring HSRP group 1 in the SW_CORE_1
    - name: Configuring switch virtual interface with HSRP in the Core SW_CORE_1
    hosts: SW_CORE_1
    gather_facts: false

    vars:
        ansible_connection: network_cli
        ansible_network_os: ios
        ansible_user: teste
        ansible_ssh_pass: teste

    tasks:    
        - name: Configurando switch virtual interface com HSRP grupo 1 no SW_CORE_1
        ios_config:        
            parents: "interface "
            lines:
            - "ip address  " 
            - "no shutdown"

            - "standby 1 ip 192.168.11.3"
            - "standby 1 preempt"
            - "standby 1 priority 120"

            - "standby 1 ip 192.168.11.67"
            - "standby 1 preempt"
            - "standby 1 priority 120"

            - "standby 1 ip 192.168.11.131"
            - "standby 1 preempt"
            - "standby 1 priority 120"

            - "standby 1 ip 192.168.11.195"
            - "standby 1 preempt"
            - "standby 1 priority 120"
            
        with_items:
            - { interface : vlan 10, address : 192.168.11.1, mask : 255.255.255.192 }
            - { interface : vlan 20, address : 192.168.11.65, mask : 255.255.255.192 }
            - { interface : vlan 30, address : 192.168.11.129, mask : 255.255.255.192 }
            - { interface : vlan 40, address : 192.168.11.193, mask : 255.255.255.192 }

        register: print_output

        #Configuring HSRP group 2 in the SW_CORE_1
        - name: Configurando switch virtual interface com HSRP grupo 2 no SW_CORE_1
        ios_config:        
            parents: "interface "
            lines:          
            - "standby 2 ip 192.168.11.4"        
            - "standby 2 preempt"
            - "standby 2 priority 110"

            - "standby 2 ip 192.168.11.68"
            - "standby 2 preempt"
            - "standby 2 priority 110"

            - "standby 2 ip 192.168.11.132"
            - "standby 2 preempt"
            - "standby 2 priority 110"

            - "standby 2 ip 192.168.11.196"
            - "standby 2 preempt"
            - "standby 2 priority 110"

        with_items:
            - { interface : vlan 10 }
            - { interface : vlan 20 }
            - { interface : vlan 30 }
            - { interface : vlan 40 }      

        register: print_output

Configurando SVIs e HSRP load balancing no SW_CORE_2:

.. code:: yaml

    #Configuring HSRP group 2 in the SW_CORE_2
    - name: Configuring switch virtual interface with HSRP Core SW_CORE_2
    hosts: SW_CORE_2
    gather_facts: false

    vars:
        ansible_connection: network_cli
        ansible_network_os: ios
        ansible_user: teste
        ansible_ssh_pass: teste

    tasks:    
        - name: Configurando switch virtual interface com HSRP grupo 2 no SW_CORE_2
        ios_config:        
            parents: "interface "
            lines:
            - "ip address  " 
            - "no shutdown"

            - "standby 2 ip 192.168.11.4"   
            - "standby 2 preempt"
            - "standby 2 priority 120"

            - "standby 2 ip 192.168.11.68"
            - "standby 2 preempt"
            - "standby 2 priority 120"

            - "standby 2 ip 192.168.11.132"
            - "standby 2 preempt"
            - "standby 2 priority 120"

            - "standby 2 ip 192.168.11.196"
            - "standby 2 preempt"
            - "standby 2 priority 120"
            
        with_items:
            - { interface : vlan 10, address : 192.168.11.2, mask : 255.255.255.192 }
            - { interface : vlan 20, address : 192.168.11.66, mask : 255.255.255.192 }
            - { interface : vlan 30, address : 192.168.11.130, mask : 255.255.255.192 }
            - { interface : vlan 40, address : 192.168.11.194, mask : 255.255.255.192 }

        register: print_output

        #Configuring HSRP group 1 in the SW_CORE_2
        - name: Configurando switch virtual interface com HSRP grupo 1 no SW_CORE_2
        ios_config:        
            parents: "interface "
            lines:          
            - "standby 1 ip 192.168.11.3"       
            - "standby 1 preempt"
            - "standby 1 priority 110"

            - "standby 1 ip 192.168.11.67"
            - "standby 1 preempt"
            - "standby 1 priority 110"

            - "standby 1 ip 192.168.11.131"
            - "standby 1 preempt"
            - "standby 1 priority 110"

            - "standby 1 ip 192.168.11.195"
            - "standby 1 preempt"
            - "standby 1 priority 110"

        with_items:
            - { interface : vlan 10 }
            - { interface : vlan 20 }
            - { interface : vlan 30 }
            - { interface : vlan 40 }      
            
        register: print_output

Bom, esses são alguns exemplos de como trabalhar com módulos ansible playbook.