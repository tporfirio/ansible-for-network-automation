Módulo ios_command 
------------------

O módulo ios_command envia comandos show para um dispositivo IOS e retorna o resultado do comando.

.. note::

    Vale ressaltar que o módulo ios_command não executa comandos no modo de configuração. Para essa tarefa você deve alocar o módulo ios_config.

Um exemplo de uso do módulo ios_command:

.. code:: yaml
 
    ---
    - name: SHOW
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

        -  debug: var=sh_run

Ao contrário do uso do módulo ios_config, o manual não indica que foram feitas alterações (changed).

Executando vários comandos 
~~~~~~~~~~~~~~~~~~~~~~~~~~

O módulo ios_command permite executar vários comandos:

.. code:: yaml
    
    ---
    - name: SHOW
      hosts: ansible_core
      gather_facts: false

      vars: # Variável de conexão
        ansible_connection: network_cli
        ansible_network_os: ios
        ansible_user: teste
        ansible_ssh_pass: teste

      tasks:

        - name: show commands
          ios_command:
            commands:
                - sh run
                - sh ip int br
                - sh cdp neighbors

          register: show_commands

        -  debug: var=show_commands
    
    

No playbook acima, três comandos são indicados, portanto a sintaxe deve ser um pouco diferente - os comandos devem ser especificados como uma lista, no formato YAML.

.. note::
    
    Se vários comandos forem enviados ao módulo, o resultado da execução dos comandos estarão alocados na variável ``show_commands`` da lista. A saída estará na ordem em que os comandos estão descritos na tarefa.
    
