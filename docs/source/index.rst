Ansible para Automação de Rede
=============================

.. Warning::

    O livro está em processo de escrita!

.. figure:: https://github.com/networkforcode/ansible-for-network-automation/blob/master/images/lab3.jpg

Ansible é um sistema de gerenciamento de configuração. O Ansible permite automatizar e simplificar a configuração, manutenção e implantação de servidores, serviços, software, etc.

No entanto, o Ansible é usado com mais frequência para trabalhar com equipamentos de rede. Isso ocorre por que o Ansible não requer a instalação de um agente em hosts gerenciados. Baseado nisso a interação com os dispositivos remotos é feita através de conexão SSH.

Além disso, o Ansible está desenvolvendo ativamente o suporte a equipamentos de rede, e novos recursos e módulos para trabalhar com equipamentos de rede estão constantemente aparecendo nele. Alguns equipamentos de rede são compatíveis com outros sistemas de gerenciamento de configuração (permitem instalar um agente). Uma das vantagens importantes do Ansible é que é fácil começar a trabalhar com ele.


.. toctree::
   :maxdepth: 2

   book/01_basics/index.rst
   book/02_playbook_basics/index.rst
   book/03_network_os_modules/index.rst
   book/04_criando_playbook/index.rst
   book/05_group_vars e host_vars/index.rst
   book/06_playbook_backup_/index.rst
