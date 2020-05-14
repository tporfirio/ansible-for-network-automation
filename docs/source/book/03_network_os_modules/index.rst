.. raw:: latex

   \newpage

.. _ansible_for_network_index:

3. Módulos de rede vinculados a um SO específico 
================================================

Esta seção discute os módulos que funcionam com equipamentos de rede por meio da CLI. Para equipamentos que funcionam apenas através da CLI, o Ansible suporta três tipos de módulos que são os módulos principais para começar a se trabalhar com o Ansible:

* os_command - executa comandos show.
* os_facts - coleta fatos sobre dispositivos.
* os_config - executa comandos de configuração.

Assim, para diferentes sistemas operacionais, haverá diferentes módulos. Por exemplo, para os módulos do Cisco IOS serão chamados:

* ios_command 
* ios_config 
* ios_facts

Módulos semelhantes aos de cima estão disponíveis para os seguintes SO: 

* Dellos10 
* Dellos6 
* Dellos9 
* EOS 
* IOS 
* IOS XR 
* JUNOS 
* SR OS 
* VyOS

Uma lista completa de todos os módulos de rede suportados pelo Ansible você encontra `aqui <http://docs.ansible.com/ansible/latest/modules/list_of_network_modules.html>`__.

.. note::
     
    O Ansible está se desenvolvendo ativamente para dar suporte ao trabalho com equipamentos de rede e, na próxima versão do Ansible, pode haver módulos adicionais. Portanto, se no momento da leitura do livro já existe a próxima versão do Ansible (versão no livro 2.9), use-a e verifique na documentação quais novos recursos e módulos apareceram.

Esta seção discute exemplos de módulos para trabalhar com o Cisco IOS:

* ios_command 
* ios_config 
* ios_facts

.. note::

    Se você examinar como trabalhar com módulos para IOS, tudo será o mesmo com outros vendors.

.. toctree::
   :maxdepth: 1

   ios_command
   ios_facts
   ios_config
