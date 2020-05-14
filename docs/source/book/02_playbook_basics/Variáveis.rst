Variáveis
==========

Uma variável consiste em: 

* Informações do dispositivo, que são coletadas como um fato através do ``gather_facts``. 
* Nas variáveis, você pode escrever a saída do comando da CLI.

Definição de variáveis
----------------------

Variáveis podem ser definidas nos seguintes locais:

* No arquivo de inventário;
* No manual;
* Em arquivos especiais baseados em um grupo de dispositivo;
* Em arquivos separados que são adicionados ao playbook via include (como no Jinja2);
* Chamando playbooks através de variáveis.

Variáveis no arquivo de inventário
-----------------------------------

No arquivo de inventário, você pode especificar variáveis para o grupo:

.. code:: ini

    [ansible_core]
    SW_CORE_1
    SW_CORE_2

    [ansible_access]
    SW_ACCESS_1
    SW_ACCESS_2
    SW_ACCESS_3
    SW_ACCESS_4

    [ansible_core:vars]
    ntp_server=192.168.70.200
    log_server=10.5.100.1

As variáveis ``ntp_server`` e ``log_server`` pertencem ao grupo ``ansible_core`` e podem ser alocadas dentro da configuração de um módulo durante a escrita de um playbook.

Variáveis alocadas no manual
----------------------------

Alocar variáveis direto no manual, tem seu lado bom e seu lado ruim. É conveniente alocar variáveis dentro do mesmo arquivo onde estão definidas as tarefas por que as variáveis estão no mesmo local que todas as ações. Porém, ao crescer esse script, as variáveis poderão ficar desorganizadas. 

Segue um exemplo de como definir variáveis no manual e chamá-las através de um parâmetro específico:

.. code:: ini

    ---

    - name: Run command 
      hosts: SW_ACCESS_1
      gather_facts: false

      vars: # Variável de conexão
        ansible_connection: network_cli
        ansible_network_os: ios
        ansible_user: teste
        ansible_ssh_pass: teste
        # Definindo variável
        vlan: sh vlan br

      tasks:

        - name: sh clock
          ios_command:
            commands: sh clock
            commands: "{{ vlan }}" # Chamando a variável

          register: print_output 

        -  debug: var=print_output.stdout_lines 
