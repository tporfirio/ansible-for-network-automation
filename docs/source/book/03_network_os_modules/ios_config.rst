Módulo Ios_config
==================

O módulo ios_config permite configurar dispositivos executando o iOS, além de gerar modelos de configuração ou enviar comandos com base no modelo.

Lines
~~~~~

A maneira mais fácil de usar o módulo ios_config é enviar comandos do modo de configuração global com o parâmetro lines Para o parâmetro lines, existem comandos de alias, ou seja, você pode escrever comandos em vez de linhas.

Exemplo:

.. code:: yaml
    
    ---

    - name: Configurando
      hosts: ansible_core
      gather_facts: false

      vars: # Variável de conexão
        ansible_connection: network_cli
        ansible_network_os: ios
        ansible_user: teste
        ansible_ssh_pass: teste

      tasks:

        - name: Config username
          ios_config:
            lines:
              - username thiago priv 15 pass thiago

Parents
~~~~~~~

O parâmetro parents é usado para indicar em qual submodo os comandos são aplicados.

Por exemplo, você precisa aplicar os seguintes comandos:

.. code:: bash
    
    SW_CORE_SW2(config)#line vty 0 4    
    SW_CORE_SW2(config-line)#login local
    SW_CORE_SW2(config-line)#transport input ssh

Nesse caso, o playbook terá a seguinte aparência:

.. code:: yaml

    
- name: Configurando SSH
  hosts: ansible_core
  gather_facts: false

  vars: # Variável de conexão
     ansible_connection: network_cli
     ansible_network_os: ios
     ansible_user: teste
     ansible_ssh_pass: teste

  tasks:

    - name: Config line vty
      ios_config:
        parents:
          - line vty 0 4
        lines:
          - login local
          - transport input ssh

.. toctree::
   :maxdepth: 1

   ios_config_lines
   ios_config_parents
   ios_config_updates
   ios_config_save_when
   ios_config_backup
   ios_config_defaults
   ios_config_after
   ios_config_before
   ios_config_match
   ios_config_replace
   ios_config_src

