Sintaxe do Playbook
------------------

Playbooks são descritos no formato YAML.


Exemplo de sintaxe do playbook
~~~~~~~~~~~~~~~~~~~~~~~~~~


Antes de processeguir para a criação de um playbook onde irá executar tarefas simples, primeiro irei alocar mais dispositivos no arquivo ``~/Documentos/Code/Ansible/lab1/hosts``:

.. code:: ine

    [ansible_core]
    SW_CORE_1
    SW_CORE_2

    [ansible_access]
    SW_ACCESS_1
    SW_ACCESS_2
    SW_ACCESS_3
    SW_ACCESS_4
    
Exemplo do playbook playbook01.yml:

.. code:: yaml

    --- # PLAYBOOK

    - name: Run show commands on devices # PLAY 1
      hosts: ansible_core
      gather_facts: false

      vars: # Variável de conexão
        ansible_connection: network_cli
        ansible_network_os: ios
        ansible_user: teste
        ansible_ssh_pass: teste

      tasks:

        - name: show ip int brief # TASK 1
          ios_command:
            commands: show ip int brief

          register: print_output 

        -  debug: var=print_output.stdout_lines

        - name: run sh ip arp # TASK 2
          ios_command:
            commands: sh ip arp

          register: print_output 

        -  debug: var=print_output.stdout_lines


    - name: Run command # PLAY 2
      hosts: SW_ACCESS_1
      gather_facts: false

      vars: # Variável de conexão
        ansible_connection: network_cli
        ansible_network_os: ios
        ansible_user: teste
        ansible_ssh_pass: teste

      tasks:

        - name: sh clock # TASK 1
          ios_command:
            commands: sh clock

          register: print_output 

        -  debug: var=print_output.stdout_lines 

.. note::
    
    Percebe-se que no código acima contém dois cenários (PLAY 1 e PLAY 2). Cada cenário é seguido de uma ou mais tasks.
    
* ``name: Run show commands on devices`` - se refere ao nome do manual alocado no primeiro cenário (PLAY 1).
* ``hosts`` - deverá inserir um dispositivo específico, grupo de dispositivos, grupos de dispositivos ou inserir o parâmetro ``all``. Esse parâmetro indica que as tasks escritas irão surgir efeito para todos os dispositivos alocados dentro do arquivo ``hosts``. 
* ``gather_facts: false`` - indica se deve ou não recolher fatos do dispositivo, fatos seria informações de hardware dos dispositivos.
* ``tasks:`` - é a onde a mágica acontece, nessa seção é descrito os comandos que você deseja enviar para os dispositivos remotos.
* ``register: print_output`` - essa variável serve para armazenar os dados executados na task.
* ``debug: var=print_output.stdout_lines`` - imprimindo os dados armazenados na variável print_output.

Depois de explicar os principais parâmetros dentro do playbook, iremos executar:

.. code:: bash

    $ ansible-playbook playbook01.yml

É assim que a execução do playbook se parece:

.. code:: yaml
    
    thiago@thiago-ThinkPad-T430:~/Documentos/Code/Ansible/lab1$ ansible-playbook playbook01.yml 

    PLAY [Run show commands on routers] ************************************************************************************

    TASK [show ip int brief] ***********************************************************************************************
    ok: [SW_CORE_2]
    ok: [SW_CORE_1]

    TASK [debug] ***********************************************************************************************************
    ok: [SW_CORE_1] => {
        "print_output.stdout_lines": [
            [
                "Interface              IP-Address      OK? Method Status                Protocol",
                "Ethernet0/0            unassigned      YES unset  up                    up      ",
                "Ethernet0/1            unassigned      YES unset  up                    up      ",
                "Ethernet0/2            unassigned      YES unset  up                    up      ",
                "Ethernet0/3            unassigned      YES unset  up                    up      ",
                "Ethernet1/0            unassigned      YES unset  up                    up      ",
                "Ethernet1/1            unassigned      YES unset  up                    up      ",
                "Ethernet1/2            unassigned      YES unset  up                    up      ",
                "Ethernet1/3            unassigned      YES unset  up                    up      ",
                "Ethernet2/0            unassigned      YES unset  up                    up      ",
                "Ethernet2/1            unassigned      YES unset  up                    up      ",
                "Ethernet2/2            unassigned      YES unset  up                    up      ",
                "Ethernet2/3            unassigned      YES unset  up                    up      ",
                "Vlan1                  192.168.36.214  YES NVRAM  up                    up"
            ]
        ]
    }
    ok: [SW_CORE_2] => {
        "print_output.stdout_lines": [
            [
                "Interface              IP-Address      OK? Method Status                Protocol",
                "Ethernet0/0            unassigned      YES unset  up                    up      ",
                "Ethernet0/1            unassigned      YES unset  up                    up      ",
                "Ethernet0/2            unassigned      YES unset  up                    up      ",
                "Ethernet0/3            unassigned      YES unset  up                    up      ",
                "Ethernet1/0            unassigned      YES unset  up                    up      ",
                "Ethernet1/1            unassigned      YES unset  up                    up      ",
                "Ethernet1/2            unassigned      YES unset  up                    up      ",
                "Ethernet1/3            unassigned      YES unset  up                    up      ",
                "Ethernet2/0            unassigned      YES unset  up                    up      ",
                "Ethernet2/1            unassigned      YES unset  up                    up      ",
                "Ethernet2/2            unassigned      YES unset  up                    up      ",
                "Ethernet2/3            unassigned      YES unset  up                    up      ",
                "Vlan1                  192.168.36.215  YES NVRAM  up                    up"
            ]
        ]
    }

    TASK [run sh ip arp] ***************************************************************************************************
    ok: [SW_CORE_1]
    ok: [SW_CORE_2]

    TASK [debug] ***********************************************************************************************************
    ok: [SW_CORE_1] => {
        "print_output.stdout_lines": [
            [
                "Protocol  Address          Age (min)  Hardware Addr   Type   Interface",
                "Internet  192.168.36.1            4   0050.56c0.0008  ARPA   Vlan1",
                "Internet  192.168.36.2            0   0050.56fb.4a64  ARPA   Vlan1",
                "Internet  192.168.36.128         54   000c.29a2.83c1  ARPA   Vlan1",
                "Internet  192.168.36.214          -   aabb.cc80.6000  ARPA   Vlan1"
            ]
        ]
    }
    ok: [SW_CORE_2] => {
        "print_output.stdout_lines": [
            [
                "Protocol  Address          Age (min)  Hardware Addr   Type   Interface",
                "Internet  192.168.36.1            4   0050.56c0.0008  ARPA   Vlan1",
                "Internet  192.168.36.2           21   0050.56fb.4a64  ARPA   Vlan1",
                "Internet  192.168.36.128         54   000c.29a2.83c1  ARPA   Vlan1",
                "Internet  192.168.36.215          -   aabb.cc80.7000  ARPA   Vlan1"
            ]
        ]
    }

    PLAY [Run command] *****************************************************************************************************

    TASK [sh clock] ********************************************************************************************************
    ok: [SW_ACCESS_1]

    TASK [debug] ***********************************************************************************************************
    ok: [SW_ACCESS_1] => {
        "print_output.stdout_lines": [
            [
                "*19:51:11.310 EET Tue May 12 2020"
            ]
        ]
    }

    PLAY RECAP *************************************************************************************************************
    SW_ACCESS_1                : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
    SW_CORE_1                  : ok=4    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
    SW_CORE_2                  : ok=4    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
    
.. note::
    
    Observe que um comando diferente é usado para iniciar o manual. Para os comandos Ad-Hoc, o comando ``ansible`` foi usado. E para o manual - ``ansible-playbook``.
