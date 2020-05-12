Módulos
==============

A biblioteca de módulos é instalada junto ao Ansible. Os módulos são responsáveis pelas ações que o Ansible executa. Além disso, cada módulo é responsável por sua tarefa específica e pequena.

Por exemplo, já executamos comandos Ad-Hoc usando o módulo ios_command e passamos argumentos para ele. Agora, iremos definir como alocar parâmetros de configuração do módulo ios_vlan dentro de um arquivo de manual (playbook), segue exemplo descrito abaixo:

.. code:: bash
    - name: Criando VLAN 15
      ios_vlan:
         - vlan_id: 15              
           name: VLAN 15          
           state: active
    
Esses parâmetro irá criar a vlan 15 nomeá-la com o nome de VLAN 15. 

Caso você queira criar duas ou mais vlans nos hosts de destino, deverá escrever o playbook com os seguintes parâmetros:

.. code:: bash
    
    - name: Criando VLANS 15 e 25
      ios_vlan:
        aggregate:
          - vlan_id: 15             
            name: VLAN 15          
            state: active

          - vlan_id: 25              
            name: VLAN 25          
            state: active

Para visualizar a lista de módulos suportados pelo Ansible, você pode verificar nessa `documentação <https://docs.ansible.com/ansible/latest/reference_appendices/config.html#common-options>`__.
