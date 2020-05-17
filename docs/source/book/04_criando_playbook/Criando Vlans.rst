Criando Vlans
-------------

Iremos montar nosso playbook para executar a task:

.. code:: yaml

    ---
    - name: Configuring devices # Nome do manual 
    hosts: all # Irá executar todos os hosts de todos os grupos que estão alocados no arquivo hosts
    gather_facts: false # Recolhe informações do dispositivo e retorna a saída em YAML
    
    vars: # Variável de conexão
        ansible_connection: network_cli
        ansible_network_os: ios
        ansible_user: teste
        ansible_ssh_pass: teste
    
    tasks:
    - name: Configurando VTP Transparent mode e NTP em todos os switches 
      ios_config: # Módulo de configuração       
        lines:
          - vtp domain ansible
          - vtp mode transparent         
        
      register: print_output # Armazenando os dados executados no módulo acima

    -  debug: var=print_output.stdout_lines # Imprimindo os dados armazenados 
    
    # Criar VLANS 10, 20, 30 e 40
    - name: Criando VLANS 10, 20, 30 e 40
      ios_vlan: # Módulos contendo apenas parametrização de vlan
        aggregate: # Executa a lista de itens ordenados pelo parâmetro vlan_id
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

A variável de conexão nada mais é que, o registro de conexão do device remoto, essas variáveis também faz a conexão de usuários cadastrados no tacacs ou radius.

.. note::

    Ao declarar minhas variáveis de comunicação, utilizei o parâmetro network_cli que se refere no modo de conexão CLI sobre SSH. Vale ressaltar que não são todos os módulos de redes que suportam esse tipo de protocolo de comunicação.

Com poucas linhas de código, podemos configurar o VTP e vlan id e replicar em todos os devices da topologia.
