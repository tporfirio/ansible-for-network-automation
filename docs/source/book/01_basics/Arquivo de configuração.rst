Arquivo de configuração
---------------------

Primeiro, você precisa criar um arquivo de configuração no diretório de sua preferência. Irei criar no diretório /home/thiago/Documentos/Code/Ansible/lab1/. Vamos chamá-lo de ansible.cfg:

.. code:: bash

    [defaults]
    inventory = ./hosts
    host_key_checking = false
    timeout = 5 

Parâmetros do arquivo ``ansible.cfg``: 

* ``[defaults]`` - se refere ao padrão de configurações gerais listadas nos valores abaixo.
* ``inventory = ./hosts`` - definindo o arquivo de inventário a ser utilizado para alocar os dispositivos que queremos interagir.
* ``host_key_checking = false`` - definindo o parâmetro false para definir que as chaves SSH não sejam trocadas ao iniciar a autenticação.
* ``timeout = 5`` - tempo limite até a conexão ser autenticada.

.. note::

    Percebe-se que o arquivo ``ansible.cfg`` contém valores simples, porém é o necessário para colocar nossos playbooks para rodar. Caso você deseja verificar uma lista completa dos parâmetros e suas descrições, você pode encontrar nessa `documentação <https://docs.ansible.com/ansible/latest/reference_appendices/config.html#common-options>`__.
