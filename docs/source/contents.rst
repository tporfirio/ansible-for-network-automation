Ansible para Automação de Rede
=============================

Ansible é um sistema de gerenciamento de configuração. O Ansible permite automatizar e simplificar a configuração, manutenção e implantação de servidores, serviços, software, etc.

No entanto, o Ansible é usado com mais frequência para trabalhar com equipamentos de rede. Isso ocorre por que o Ansible não requer a instalação de um agente em hosts gerenciados. Baseado nisso a interação com os dispositivos remotos é feita através de conexão SSH.

Além disso, o Ansible está desenvolvendo ativamente o suporte a equipamentos de rede, e novos recursos e módulos para trabalhar com equipamentos de rede estão constantemente aparecendo nele. Alguns equipamentos de rede são compatíveis com outros sistemas de gerenciamento de configuração (permitem instalar um agente). Uma das vantagens importantes do Ansible é que é fácil começar a trabalhar com ele.


.. toctree::
   :maxdepth: 2

   book/01_basics/index.rst
   book/02_playbook_basics_/index.rst
   book/03_network_os_modules_/index.rst
   book/04_network_resource_modules_/index.rst
   book/05_network_cli_modules_/index.rst
   book/06_parsing_output_/index.rst
   book/07_playbooks_/index.rst
