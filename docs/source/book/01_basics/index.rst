.. raw:: latex

   \newpage

.. _ansible_basics_index:

1. Ansible Fundamentos
============================

Ansible: 

* Funciona sem instalar o agente em hosts gerenciados.
* Usa SSH para conectar-se a hosts gerenciados. 
* Executa alterações usando módulos Python que são executados em hosts gerenciados.
* Pode executar ações localmente no host de gerenciamento.
* Usa YAML para descrever scripts.
* Contém muitos módulos (seu número está aumentando constantemente).
* Você pode escrever seus próprios módulos.

Тerminologia:

-  **Control node** — o host de gerenciamento. Servidor possível a partir do qual outros hosts são gerenciados.
-  **Managed nodes** — são hosts que so gerenciados pelo control node.
-  **Inventory** — é o arquivo onde são armazenados dados dos hosts remotos.
-  **Playbook** — se refere ao manual onde as tasks são escritas.
-  **Task** — é uma variável onde são alocados parâmetros de configuração e verificação.
-  **Module** — são pacotes comprimidos baseados no nível de configuração de cada SO, por exemplo, desejo enviar configurações para os devices remotos (Cisco) e quero apenas atingirar a camada de configuração (config), para este exemplo, devo me basear no módulo ios_config.

A lista completa dos termos você encontra nessa
`documentação <http://docs.ansible.com/ansible/devel/glossary.html>`__.

.. toctree::
   :maxdepth: 1

   Instalação
   inventário
   Comandos Ad-Hoc
   Configuração
   Módulos
   network_cli
