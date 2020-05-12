.. raw:: latex

   \newpage

.. _ansible_basics_index:

2. Noções básicas de playbooks
===================

Playbook (arquivo de script) é um arquivo que descreve as ações que precisam ser executadas em um grupo de hosts.

Principais parâmetros alocadas dentro do playbook: 

* hosts - neste parâmetro deverá inserir um host em específico ou um grupo de hosts no qual você deseja enviar tarefas. 
* task - é baseada em módulos, ao especificar o módulo, deverá inserir os parâmetros complimentares que fazem parte do módulo escolhido para trabalhar.

.. note::
    
    Uma task pode-se trabalhar com diversos módulos sendo executados de modo sequêncial de tarefas, segue exemplo mostrado abaixo:
    
.. code:: yaml

     tasks:
    - name: Configurando VTP Transparent mode e NTP em todos os switches 
      ios_config: # Módulo de configuração       
        lines:
          - vtp domain ansible
          - vtp mode transparent         
        
      register: print_output # Armazenando os dados executados no módulo acima    

      # Create VLANS
    - name: Criando VLANS 10, 20, 30 e 40
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

.. toctree::
   :maxdepth: 1

   Sintaxe do playbook
   Variáveis
   Trabalhar com resultados de execução do módulo
