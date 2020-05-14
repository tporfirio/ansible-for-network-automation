Trabalhar com resultados de execução do módulo
---------------------------------------

Esta seção discute métodos que permitem imprimir a saída do comando executado nos dispositivos:

* register 
* debug
* when

register
~~~~~~~

O parâmetro **register** salva o resultado da execução de um ou mais comandos ou um módulo de configuração específica e armazena em uma variável. Essa variável pode ser usada para exibir a saída do comando durante o andamento de execução do playbook.

No playbook abaixo, usando o parâmetro **register**, a saída do comando do módulo de configuração de vlan é salva na variável **print_output**:

.. code:: yaml
    
    ---
    
    - name: VLANS
      hosts: all
      gather_facts: false
      
      vars:
        ansible_connection: network_cli
        ansible_network_os: ios
        ansible_user: teste
        ansible_ssh_pass: teste
      
      tasks:
        - name: Criando Vlans
          ios_vlan:
            aggregate:
              - vlan_id: 10              
                name: VLAN 10          
                state: active

              - vlan_id: 20              
                name: VLAN 20          
                state: active 

              - vlan_id: 30              
                name: VLAN 30          
                state: active

              - vlan_id: 40              
                name: VLAN 40          
                state: active          

          register: print_output

.. note::
    
    Se você executar este manual, a saída não será diferente, pois, a saída do comando é armazenada apenas na variável **print_output**. Para que possamos visualizar a saída impressa durante a execução do script, devemos alocar o módulo de debug.
    
debug
~~~~~

Este módulo imprime os comandos executados e armazanados dentro do módulo **register** e imprime a saída do comando durante a execução do playbook.

Abaixo está um exemplo de como alocar o módulo **debug** dentro do playbook:

.. code:: yaml
    
    ---
    
    - name: VLANS
      hosts: all
      gather_facts: false
      
      vars:
        ansible_connection: network_cli
        ansible_network_os: ios
        ansible_user: teste
        ansible_ssh_pass: teste
      
      tasks:
        - name: Criando Vlans
          ios_vlan:
            aggregate:
              - vlan_id: 10              
                name: VLAN 10          
                state: active

              - vlan_id: 20              
                name: VLAN 20          
                state: active 

              - vlan_id: 30              
                name: VLAN 30          
                state: active

              - vlan_id: 40              
                name: VLAN 40          
                state: active          

          register: print_output
       
        - debug: var=print_output.stdout_lines

A variável **print_output** mostra a saída do comando em formato JSON.
    
O resultado da execução do manual acima se parece com o seguinte:

.. code:: json

    thiago@thiago-ThinkPad:~/Documentos/Code/Ansible/lab1$ ansible-playbook vlan.yml 

    PLAY [VLANS] ***********************************************************************************************************

    TASK [Criando Vlans] ***************************************************************************************************
    changed: [SW_CORE_1]
    changed: [SW_CORE_2]

    TASK [debug] ***********************************************************************************************************
    ok: [SW_CORE_1] => {
        "print_output": {
            "ansible_facts": {
                "discovered_interpreter_python": "/usr/bin/python"
            },
            "changed": true,
            "commands": [
                "vlan 10",
                "name Vlan 10",
                "state active",
                "vlan 20",
                "name Vlan 20",
                "state active",
                "vlan 30",
                "name Vlan 30",
                "state active",
                "vlan 40",
                "name Vlan 40",
                "state active"
            ],
            "deprecations": [
                {
                    "msg": "Distribution Ubuntu 18.04 on host SW_CORE_1 should use /usr/bin/python3, but is using
                    /usr/bin/python for backward compatibility with prior Ansible releases. A future Ansible release
                    will default to using the discovered platform python for this host. See
                    https://docs.ansible.com/ansible/2.9/reference_appendices/interpreter_discovery.html for more
                    information",
                    "version": "2.12"
                }
            ],
            "failed": false,
            "warnings": [
                "The value 10 (type int) in a string field was converted to '10' (type string). If this does not look 
                like what you expect, quote the entire value to ensure it does not change.",
                "The value 20 (type int) in a string field was converted to '20' (type string). If this does not look 
                like what you expect, quote the entire value to ensure it does not change.",
                "The value 30 (type int) in a string field was converted to '30' (type string). If this does not look 
                like what you expect, quote the entire value to ensure it does not change.",
                "The value 40 (type int) in a string field was converted to '40' (type string). If this does not look 
                like what you expect, quote the entire value to ensure it does not change."
            ]
        }
    }
    ok: [SW_CORE_2] => {
        "print_output": {
            "ansible_facts": {
                "discovered_interpreter_python": "/usr/bin/python"
            },
            "changed": true,
            "commands": [
                "vlan 10",
                "name Vlan 10",
                "state active",
                "vlan 20",
                "name Vlan 20",
                "state active",
                "vlan 30",
                "name Vlan 30",
                "state active",
                "vlan 40",
                "name Vlan 40",
                "state active"
            ],
            "deprecations": [
                {
                    "msg": "Distribution Ubuntu 18.04 on host SW_CORE_2 should use /usr/bin/python3, but is using /usr/bin/python for backward compatibility with prior Ansible releases. A future Ansible release will default to using the discovered platform python for this host. See https://docs.ansible.com/ansible/2.9/reference_appendices/interpreter_discovery.html for more information",
                    "version": "2.12"
                }
            ],
            "failed": false,
            "warnings": [
                "The value 10 (type int) in a string field was converted to '10' (type string). If this does not look like what you expect, quote the entire value to ensure it does not change.",
                "The value 20 (type int) in a string field was converted to '20' (type string). If this does not look like what you expect, quote the entire value to ensure it does not change.",
                "The value 30 (type int) in a string field was converted to '30' (type string). If this does not look like what you expect, quote the entire value to ensure it does not change.",
                "The value 40 (type int) in a string field was converted to '40' (type string). If this does not look like what you expect, quote the entire value to ensure it does not change."
            ]
        }
    }

    PLAY RECAP *************************************************************************************************************
    SW_CORE_1                  : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
    SW_CORE_2                  : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   

when
~~~~

O uso do parâmetro **when** permite especificar a condição sob a qual a tarefa é executada. Se a condição não for atendida, a tarefa será ignorada.

Segue um exemplo de onde alocar o parâmetro **when**:

.. code::
    
    ---
    
    - name: SHOW RUN
      hosts: ansible_core
      gather_facts: false

      vars: # Variável de conexão
        ansible_connection: network_cli
        ansible_network_os: ios
        ansible_user: teste
        ansible_ssh_pass: teste

      tasks:

        - name: sh run
          ios_command:
            commands: sh run
          register: sh_run

        - name: Debug registered var
          debug: 
            msg: "task executada"
          when: "'sbrurbles' not in sh_run.stdout[0]"

Ao executar o playbook acima, tivemos o seguinte retorno:

.. code::
    
    thiago@thiago-ThinkPad:~/Documentos/Code/Ansible/lab1$ ansible-playbook when.yml

    PLAY [SHOW RUN] ********************************************************************************************************

    TASK [sh run] **********************************************************************************************************
    ok: [SW_CORE_2]
    ok: [SW_CORE_1]

    TASK [Debug registered var] ********************************************************************************************
    skipping: [SW_CORE_2]
    skipping: [SW_CORE_1]

    PLAY RECAP *************************************************************************************************************
    SW_CORE_1                  : ok=1    changed=0    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0   
    SW_CORE_2                  : ok=1    changed=0    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0   

Percebe-se que tivemos o valor **skipping** impresso durante a execução do playbook, isso significa que a tarefa não foi concluída por que a condição **when** não foi atendida.

Ao excluir o parâmetro **when**, iremos ter a execução da task. Segue a execução do playbook novamente:

.. code::

    thiago@thiago-ThinkPad:~/Documentos/Code/Ansible/lab1$ ansible-playbook when.yml

    PLAY [SHOW RUN] ********************************************************************************************************

    TASK [sh run] **********************************************************************************************************
    ok: [SW_CORE_2]
    ok: [SW_CORE_1]

    TASK [Debug registered var] ********************************************************************************************
    ok: [SW_CORE_1] => {
        "msg": "task executada"
    }
    ok: [SW_CORE_2] => {
        "msg": "task executada"
    }

    PLAY RECAP (************************************************************************************************************
    SW_CORE_1                  : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
    SW_CORE_2                  : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
      
