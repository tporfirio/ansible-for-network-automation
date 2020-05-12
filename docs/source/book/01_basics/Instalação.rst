Instalação
-----------------

O Ansible deve ser instalado apenas na máquina com a qual o gerenciamento do dispositivo será executado.

Requisitos de host de gerenciamento:

* Suporte para Python 3 (testado em 3.8)
* O Windows não pode ser o host de controle.

.. note::

    O livro usa o Ansible versão 2.9


O Ansible é atualizado com bastante frequência; portanto, é melhor instalá-lo em um ambiente virtual. Novas versões são lançadas aproximadamente a cada seis meses.

Iremos utilizar o parâmetro pip para instalar o Ansible:

::

    $ pip install ansible
