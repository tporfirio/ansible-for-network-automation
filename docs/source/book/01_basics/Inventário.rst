Inventário
----------------

Um arquivo de inventário é um arquivo que descreve os dispositivos aos quais o Ansible se conectará.

Hosts e grupos
~~~~~~~~~~~~~~

No arquivo de inventário, os dispositivos podem ser especificados através dos endereços IP ou nomes. Os dispositivos podem ser especificados um de cada vez ou divididos em grupos.

Hosts file - arquivo inventário de exemplo, pode ser escrito em .INI, sem extensão ou em formato de YAML:

.. code:: ini

    [ansible_core]
    SW_CORE_1
    SW_CORE_2

    [ansible_access]
    SW_ACCESS_1
    SW_ACCESS_2
    SW_ACCESS_3
    SW_ACCESS_4
    
O nome indicado entre colchetes é o nome do grupo. Nesse caso, dois grupos de dispositivos são criados: ansible_core e ansible_access.

.. note::

    No arquivo hosts, o mesmo endereço IP ou nome (especificando o host) pode ser alocado em grupos diferentes.

Por padrão, o arquivo hosts é localizado em ``/etc/ansible/hosts``.

Um grupo de grupos
~~~~~~~~~~~~~~~~~~~

O Ansible também permite combinar grupos de dispositivos em um grupo comum. Uma sintaxe especial é usada para isso:

.. code:: ini

    [ansible_core]
    SW_CORE_1
    SW_CORE_2

    [ansible_access]
    SW_ACCESS_1
    SW_ACCESS_2
    SW_ACCESS_3
    SW_ACCESS_4

    [cisco_devices:children]
    ansible_access
    ansible_core

Arquivo Linux ``/etc/hosts``
~~~~~~~~~~~~~~~~~~~

Esse é o arquivo hosts do linux, neste arquivo são armazenados dados dos hosts considerados locais. Ao preencher hostname e IP neste arquivo, meu host local irá conhecer esses hosts remotos como locais, segue exemplo deste arquivo:

.. code:: bash

    127.0.0.1	localhost
    127.0.1.1	thiago-ThinkPad

    # The following lines are desirable for IPv6 capable hosts
    ::1     ip6-localhost ip6-loopback
    fe00::0 ip6-localnet
    ff00::0 ip6-mcastprefix
    ff02::1 ip6-allnodes
    ff02::2 ip6-allrouters

    192.168.36.214 SW_CORE_1
    192.168.36.215 SW_CORE_2

    192.168.36.210 SW_ACCESS_1
    192.168.36.211 SW_ACCESS_2
    192.168.36.212 SW_ACCESS_3
    192.168.36.213 SW_ACCESS_4

    # LAB CAMPUS NETWORK

    192.168.36.129 SW6_DISTR
    192.168.36.130 SW5_DISTR
    192.168.36.131 SW4_DISTR
    192.168.36.132 SW3_DISTR
    192.168.36.133 SW2_DISTR
    192.168.36.134 SW1_DISTR
