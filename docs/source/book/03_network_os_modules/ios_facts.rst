Мódulo ios_facts
----------------

O módulo ios_facts coleta informações de dispositivos executando o iOS. As informações são obtidas dos seguintes comandos:

* dir 
* show version 
* show memory statistics 
* show interfaces 
* show ipv6 interface 
* show lldp
* show lldp neighbors detail 
* show running-config

Colete todos os fatos:

.. code::

    - ios_facts:
        gather_subset: all

Crie apenas um subconjunto de interfaces, ou seja, mostra apenas fatos das interfaces:

.. code::

    - ios_facts:
        gather_subset:
          - interfaces

Colete tudo, exceto o hardware:

.. code::

    - ios_facts:
        gather_subset:
          - "!hardware"

O Ansible pode coletar os seguintes fatos:

* **ansible_net_all_ipv4_addresses** - lista de endereços IPv4 no dispositivo.
* **ansible_net_all_ipv6_addresses** - lista de endereços IPv6 no dispositivo.
* **ansible_net_config** - configuração (para execução Cisco sh run).
* **ansible_net_filesystems** - sistema de arquivos do dispositivo.
* **ansible_net_gather_subset** -quais informações são coletadas (hardware, padrão, interfaces, configuração).
* **ansible_net_hostname** - nome do dispositivo.
* **ansible_net_image** - nome e caminho do SO.
* **ansible_net_interfaces** - um dicionário com todas as interfaces de dispositivos. Os nomes de interface são chaves e os dados são parâmetros de cada interface.
* **ansible_net_memfree_mb** - quantidade de memória livre no dispositivo.
* **ansible_net_memtotal_mb** - quanta memória há no dispositivo
* **ansible_net_model** - modelo do dispositivo 
* **ansible_net_serialnum** - número de série
* **ansible_net_version** - versão do IOS

Exemplo de uso do módulo ios_facts
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

No playbook descrito abaixo, todos os fatos serão mostrados ao executar o playbook:

.. code:: yaml

    ---

    - name: Collect IOS facts
      hosts: SW_ACCESS_1

      tasks:

        - name: Facts
          ios_facts:
            gather_subset: all

Ao executar o playbook acima, tivemos o seguinte retorno:

.. code:: bash
    
    thiago@thiago-ThinkPad:~/Documentos/Code/Ansible/lab1$ ansible-playbook facts.yml 

    PLAY [Collect IOS facts] *********************************************************************************************

    TASK [Facts] ***********************************************************************************************************
    ok: [SW_CORE_1]
    ok: [SW_CORE_2]

    PLAY RECAP *************************************************************************************************************
    SW_CORE_1                  : ok=1    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
    SW_CORE_2                  : ok=1    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
    
Para ver exatamente quais fatos são coletados no dispositivo, você pode adicionar o parãmetro ``-v``, as informações serão impressa de forma resumida:

.. code::
    
    thiago@thiago-ThinkPad:~/Documentos/Code/Ansible/lab1$ ansible-playbook facts.yml -v
    Using /home/thiago/Documentos/Code/Ansible/lab1/ansible.cfg as config file

    PLAY [Collect IOS facts] ***********************************************************************************************

    TASK [Facts] ***********************************************************************************************************
    [WARNING]: default value for `gather_subset` will be changed to `min` from `!config` v2.11 onwards
    ok: [SW_CORE_1] => {"ansible_facts": {"ansible_net_all_ipv4_addresses": ["192.168.36.214"], "ansible_net_all_ipv6_addresses": [], "ansible_net_api": "cliconf", "ansible_net_config": "!\n! Last configuration change at 18:58:25 EET Thu May 14 2020\n!\nversion 15.2\nservice timestamps debug datetime msec\nservice timestamps log datetime msec\nno service password-encryption\nservice compress-config\n!\nhostname SW_CORE_1\n!\nboot-start-marker\nboot-end-marker\n!\n!\n!\nusername teste privilege 15 password 0 teste\nno aaa new-model\nclock timezone EET 2 0\n!\n!\n!\n!\n!\nvtp domain ansible\nvtp mode transparent\n!\n!\n!\nip domain-name ansible\nip cef\nno ipv6 cef\n!\n!\n!\nspanning-tree mode rapid-pvst\nspanning-tree extend system-id\n!\nvlan internal allocation policy ascending\n!\nvlan 10\n name VLAN 10\n!\nvlan 15 \n!\nvlan 20\n name VLAN 20\n!\nvlan 30\n name VLAN 30\n!\nvlan 40\n name VLAN 40\n!\nvlan 50\n name thiago\n!\nvlan 80 \n!\nvlan 90\n name VLAN 90\n!\nvlan 100\n name Vlan 100\n!\nvlan 110\n name Vlan 110\n!\nvlan 150,200 \n!\n! \n!\n!\n!\n!\n!\n!\n!\n!\n!\n!\n!\n!\ninterface Ethernet0/0\n!\ninterface Ethernet0/1\n!\ninterface Ethernet0/2\n!\ninterface Ethernet0/3\n!\ninterface Ethernet1/0\n!\ninterface Ethernet1/1\n!\ninterface Ethernet1/2\n!\ninterface Ethernet1/3\n!\ninterface Ethernet2/0\n!\ninterface Ethernet2/1\n!\ninterface Ethernet2/2\n!\ninterface Ethernet2/3\n!\ninterface Vlan1\n ip address 192.168.36.214 255.255.255.0\n!\nip forward-protocol nd\n!\nno ip http server\nno ip http secure-server\n!\n!\n!\n!\n!\n!\ncontrol-plane\n!\n!\nline con 0\n logging synchronous\nline aux 0\nline vty 0 4\n login local\n transport input ssh\n!\n!\nend", "ansible_net_filesystems": ["unix:"], "ansible_net_filesystems_info": {"unix:": {"spacefree_kb": 2097148.0, "spacetotal_kb": 2097148.0}}, "ansible_net_gather_network_resources": [], "ansible_net_gather_subset": ["interfaces", "config", "hardware", "default"], "ansible_net_hostname": "SW_CORE_1", "ansible_net_image": "unix:/opt/unetlab/addons/iol/bin/L2-ADVENTERPRISEK9-M-15.2-IRON-20151", "ansible_net_interfaces": {"Ethernet0/0": {"bandwidth": 10000, "description": null, "duplex": null, "ipv4": [], "lineprotocol": null, "macaddress": "aabb.cc00.6000", "mediatype": "unknown", "mtu": 1500, "operstatus": "up", "type": "AmdP2"}, "Ethernet0/1": {"bandwidth": 10000, "description": null, "duplex": null, "ipv4": [], "lineprotocol": null, "macaddress": "aabb.cc00.6010", "mediatype": "unknown", "mtu": 1500, "operstatus": "up", "type": "AmdP2"}, "Ethernet0/2": {"bandwidth": 10000, "description": null, "duplex": null, "ipv4": [], "lineprotocol": null, "macaddress": "aabb.cc00.6020", "mediatype": "unknown", "mtu": 1500, "operstatus": "up", "type": "AmdP2"}, "Ethernet0/3": {"bandwidth": 10000, "description": null, "duplex": null, "ipv4": [], "lineprotocol": null, "macaddress": "aabb.cc00.6030", "mediatype": "unknown", "mtu": 1500, "operstatus": "up", "type": "AmdP2"}, "Ethernet1/0": {"bandwidth": 10000, "description": null, "duplex": null, "ipv4": [], "lineprotocol": null, "macaddress": "aabb.cc00.6001", "mediatype": "unknown", "mtu": 1500, "operstatus": "up", "type": "AmdP2"}, "Ethernet1/1": {"bandwidth": 10000, "description": null, "duplex": null, "ipv4": [], "lineprotocol": null, "macaddress": "aabb.cc00.6011", "mediatype": "unknown", "mtu": 1500, "operstatus": "up", "type": "AmdP2"}, "Ethernet1/2": {"bandwidth": 10000, "description": null, "duplex": null, "ipv4": [], "lineprotocol": null, "macaddress": "aabb.cc00.6021", "mediatype": "unknown", "mtu": 1500, "operstatus": "up", "type": "AmdP2"}, "Ethernet1/3": {"bandwidth": 10000, "description": null, "duplex": null, "ipv4": [], "lineprotocol": null, "macaddress": "aabb.cc00.6031", "mediatype": "unknown", "mtu": 1500, "operstatus": "up", "type": "AmdP2"}, "Ethernet2/0": {"bandwidth": 10000, "description": null, "duplex": null, "ipv4": [], "lineprotocol": null, "macaddress": "aabb.cc00.6002", "mediatype": "unknown", "mtu": 1500, "operstatus": "up", "type": "AmdP2"}, "Ethernet2/1": {"bandwidth": 10000, "description": null, "duplex": null, "ipv4": [], "lineprotocol": null, "macaddress": "aabb.cc00.6012", "mediatype": "unknown", "mtu": 1500, "operstatus": "up", "type": "AmdP2"}, "Ethernet2/2": {"bandwidth": 10000, "description": null, "duplex": null, "ipv4": [], "lineprotocol": null, "macaddress": "aabb.cc00.6022", "mediatype": "unknown", "mtu": 1500, "operstatus": "up", "type": "AmdP2"}, "Ethernet2/3": {"bandwidth": 10000, "description": null, "duplex": null, "ipv4": [], "lineprotocol": null, "macaddress": "aabb.cc00.6032", "mediatype": "unknown", "mtu": 1500, "operstatus": "up", "type": "AmdP2"}, "Vlan1": {"bandwidth": 1000000, "description": null, "duplex": null, "ipv4": [{"address": "192.168.36.214", "subnet": "24"}], "lineprotocol": "up", "macaddress": "aabb.cc80.6000", "mediatype": null, "mtu": 1500, "operstatus": "up", "type": "Ethernet SVI"}}, "ansible_net_iostype": "IOS", "ansible_net_memfree_mb": 848213.8203125, "ansible_net_memtotal_mb": 934130.734375, "ansible_net_neighbors": {"Ethernet0/0": [{"host": "SW_ACCESS_1.ansible", "port": "Ethernet1/0"}]}, "ansible_net_python_version": "3.6.9", "ansible_net_serialnum": "67108960", "ansible_net_system": "ios", "ansible_net_version": "15.2(CML_NIGHTLY_20151103)FLO_DSGS7", "ansible_network_resources": {},     "discovered_interpreter_python": "/usr/bin/python"}, "changed": false}
    ok: [SW_CORE_2] => {"ansible_facts": {"ansible_net_all_ipv4_addresses": ["192.168.36.215"], "ansible_net_all_ipv6_addresses": [], "ansible_net_api": "cliconf", "ansible_net_config": "!\n! Last configuration change at 18:58:25 EET Thu May 14 2020\n!\nversion 15.2\nservice timestamps debug datetime msec\nservice timestamps log datetime msec\nno service password-encryption\nservice compress-config\n!\nhostname SW_CORE_2\n!\nboot-start-marker\nboot-end-marker\n!\n!\n!\nusername teste privilege 15 password 0 teste\nno aaa new-model\nclock timezone EET 2 0\n!\n!\n!\n!\n!\nvtp domain ansible\nvtp mode transparent\n!\n!\n!\nip domain-name ansible\nip cef\nno ipv6 cef\n!\n!\n!\nspanning-tree mode rapid-pvst\nspanning-tree extend system-id\n!\nvlan internal allocation policy ascending\n!\nvlan 10\n name VLAN 10\n!\nvlan 15 \n!\nvlan 20\n name VLAN 20\n!\nvlan 30\n name VLAN 30\n!\nvlan 40\n name VLAN 40\n!\nvlan 50\n name thiago\n!\nvlan 80\n name VLAN 80\n!\nvlan 90\n name VLAN 90\n!\nvlan 100\n name Vlan 100\n!\nvlan 110\n name Vlan 110\n!\nvlan 150,200 \n!\n! \n!\n!\n!\n!\n!\n!\n!\n!\n!\n!\n!\n!\ninterface Ethernet0/0\n!\ninterface Ethernet0/1\n!\ninterface Ethernet0/2\n!\ninterface Ethernet0/3\n!\ninterface Ethernet1/0\n!\ninterface Ethernet1/1\n!\ninterface Ethernet1/2\n!\ninterface Ethernet1/3\n!\ninterface Ethernet2/0\n!\ninterface Ethernet2/1\n!\ninterface Ethernet2/2\n!\ninterface Ethernet2/3\n!\ninterface Vlan1\n ip address 192.168.36.215 255.255.255.0\n!\nip forward-protocol nd\n!\nno ip http server\nno ip http secure-server\n!\n!\n!\n!\n!\n!\ncontrol-plane\n!\n!\nline con 0\n logging synchronous\nline aux 0\nline vty 0 4\n login local\n transport input ssh\n!\n!\nend", "ansible_net_filesystems": ["unix:"], "ansible_net_filesystems_info": {"unix:": {"spacefree_kb": 2097148.0, "spacetotal_kb": 2097148.0}}, "ansible_net_gather_network_resources": [], "ansible_net_gather_subset": ["interfaces", "default", "hardware", "config"], "ansible_net_hostname": "SW_CORE_2", "ansible_net_image": "unix:/opt/unetlab/addons/iol/bin/L2-ADVENTERPRISEK9-M-15.2-IRON-20151", "ansible_net_interfaces": {"Ethernet0/0": {"bandwidth": 10000, "description": null, "duplex": null, "ipv4": [], "lineprotocol": null, "macaddress": "aabb.cc00.7000", "mediatype": "unknown", "mtu": 1500, "operstatus": "up", "type": "AmdP2"}, "Ethernet0/1": {"bandwidth": 10000, "description": null, "duplex": null, "ipv4": [], "lineprotocol": null, "macaddress": "aabb.cc00.7010", "mediatype": "unknown", "mtu": 1500, "operstatus": "up", "type": "AmdP2"}, "Ethernet0/2": {"bandwidth": 10000, "description": null, "duplex": null, "ipv4": [], "lineprotocol": null, "macaddress": "aabb.cc00.7020", "mediatype": "unknown", "mtu": 1500, "operstatus": "up", "type": "AmdP2"}, "Ethernet0/3": {"bandwidth": 10000, "description": null, "duplex": null, "ipv4": [], "lineprotocol": null, "macaddress": "aabb.cc00.7030", "mediatype": "unknown", "mtu": 1500, "operstatus": "up", "type": "AmdP2"}, "Ethernet1/0": {"bandwidth": 10000, "description": null, "duplex": null, "ipv4": [], "lineprotocol": null, "macaddress": "aabb.cc00.7001", "mediatype": "unknown", "mtu": 1500, "operstatus": "up", "type": "AmdP2"}, "Ethernet1/1": {"bandwidth": 10000, "description": null, "duplex": null, "ipv4": [], "lineprotocol": null, "macaddress": "aabb.cc00.7011", "mediatype": "unknown", "mtu": 1500, "operstatus": "up", "type": "AmdP2"}, "Ethernet1/2": {"bandwidth": 10000, "description": null, "duplex": null, "ipv4": [], "lineprotocol": null, "macaddress": "aabb.cc00.7021", "mediatype": "unknown", "mtu": 1500, "operstatus": "up", "type": "AmdP2"}, "Ethernet1/3": {"bandwidth": 10000, "description": null, "duplex": null, "ipv4": [], "lineprotocol": null, "macaddress": "aabb.cc00.7031", "mediatype": "unknown", "mtu": 1500, "operstatus": "up", "type": "AmdP2"}, "Ethernet2/0": {"bandwidth": 10000, "description": null, "duplex": null, "ipv4": [], "lineprotocol": null, "macaddress": "aabb.cc00.7002", "mediatype": "unknown", "mtu": 1500, "operstatus": "up", "type": "AmdP2"}, "Ethernet2/1": {"bandwidth": 10000, "description": null, "duplex": null, "ipv4": [], "lineprotocol": null, "macaddress": "aabb.cc00.7012", "mediatype": "unknown", "mtu": 1500, "operstatus": "up", "type": "AmdP2"}, "Ethernet2/2": {"bandwidth": 10000, "description": null, "duplex": null, "ipv4": [], "lineprotocol": null, "macaddress": "aabb.cc00.7022", "mediatype": "unknown", "mtu": 1500, "operstatus": "up", "type": "AmdP2"}, "Ethernet2/3": {"bandwidth": 10000, "description": null, "duplex": null, "ipv4": [], "lineprotocol": null, "macaddress": "aabb.cc00.7032", "mediatype": "unknown", "mtu": 1500, "operstatus": "up", "type": "AmdP2"}, "Vlan1": {"bandwidth": 1000000, "description": null, "duplex": null, "ipv4": [{"address": "192.168.36.215", "subnet": "24"}], "lineprotocol": "up", "macaddress": "aabb.cc80.7000", "mediatype": null, "mtu": 1500, "operstatus": "up", "type": "Ethernet SVI"}}, "ansible_net_iostype": "IOS", "ansible_net_memfree_mb": 848213.8203125, "ansible_net_memtotal_mb": 934130.734375, "ansible_net_neighbors": {"Ethernet0/0": [{"host": "SW_ACCESS_1.ansible", "port": "Ethernet1/1"}]}, "ansible_net_python_version": "3.6.9", "ansible_net_serialnum": "67108976", "ansible_net_system": "ios", "ansible_net_version": "15.2(CML_NIGHTLY_20151103)FLO_DSGS7", "ansible_network_resources": {}, "discovered_interpreter_python": "/usr/bin/python"}, "changed": false}

    PLAY RECAP *************************************************************************************************************
    SW_CORE_1                  : ok=1    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
    SW_CORE_2                  : ok=1    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   

Depois que o Ansible coleta os fatos do dispositivo, todos os fatos ficam disponíveis como variáveis no playbook.

Por exemplo, você pode exibir o conteúdo de um fato usando ``debug``:

.. code:: yaml

    ---
    - name: Collect IOS facts
      hosts: ansible_core
      gather_facts: false

      vars: # Variável de conexão
        ansible_connection: network_cli
        ansible_network_os: ios
        ansible_user: teste
        ansible_ssh_pass: teste

      tasks:

        - name: Facts
          ios_facts:
            gather_subset: all

        - name: Show ansible_net_all_ipv4_addresses fact
          debug: var=ansible_net_all_ipv4_addresses

        - name: Show ansible_net_interfaces fact
          debug: var=ansible_net_interfaces['Ethernet0/0']

O resultado do manual:

.. code:: bash
    
    thiago@thiago-ThinkPad:~/Documentos/Code/Ansible/lab1$ ansible-playbook facts.yml -v
    Using /home/thiago/Documentos/Code/Ansible/lab1/ansible.cfg as config file

    PLAY [Collect IOS facts] ***********************************************************************************************
    
    TASK [Show ansible_net_all_ipv4_addresses fact] ************************************************************************
    ok: [SW_CORE_1] => {
        "ansible_net_all_ipv4_addresses": [
            "192.168.36.214"
        ]
    }
    ok: [SW_CORE_2] => {
        "ansible_net_all_ipv4_addresses": [
            "192.168.36.215"
        ]
    }

    TASK [Show ansible_net_interfaces fact] ******************************************************************************************
    ok: [SW_CORE_1] => {
        "ansible_net_interfaces['Ethernet0/0']": {
            "bandwidth": 10000,
            "description": null,
            "duplex": null,
            "ipv4": [],
            "lineprotocol": null,
            "macaddress": "aabb.cc00.6000",
            "mediatype": "unknown",
            "mtu": 1500,
            "operstatus": "up",
            "type": "AmdP2"
        }
    }
    ok: [SW_CORE_2] => {
        "ansible_net_interfaces['Ethernet0/0']": {
            "bandwidth": 10000,
            "description": null,
            "duplex": null,
            "ipv4": [],
            "lineprotocol": null,
            "macaddress": "aabb.cc00.7000",
            "mediatype": "unknown",
            "mtu": 1500,
            "operstatus": "up",
            "type": "AmdP2"
        }
    }

    PLAY RECAP ***********************************************************************************************************************
    SW_CORE_1                  : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
    SW_CORE_2                  : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
