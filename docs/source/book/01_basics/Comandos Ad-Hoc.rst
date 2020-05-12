Comandos Ad-Hoc
~~~~~~~~~~~~~~

Comandos Ansible Ad-Hoc é um meio mais rápido de fazer alguma tarefa ou verificar alguma configuração sem a necessidade de criar um playbook.

Essa opção é usada nos casos em que você precisa verificar algo ou executar alguma ação única que não precise ser salva. De qualquer forma, esta é uma maneira fácil e rápida de começar a usar o Ansible.

Primeiro, você precisa criar um arquivo de inventário no diretório de sua preferência ou poderá utilizar o arquivo armazenado no diretório padrão ``/etc/ansible/hosts``. Irei criar no diretório ``/home/thiago/Documentos/Code/Ansible/lab1/``.  Vamos chamá-lo de hosts:

.. code:: ini

    [ansible_core]
    SW_CORE_1
    SW_CORE_2

A primeiro momento, ao conectar-se aos dispsitivos remotos, é melhor conectar-se a eles manualmente, para que as chaves do dispositivo sejam salvas localmente. 

Exemplo do comando Ad-Hoc:

.. code:: bash

    $ ansible SW_CORE_1 -m raw -a "show vlan brief" -u teste -k

Vamos entender os parâmetros do comando acima: 

* ``SW_CORE_1`` - dispositivo ao qual você deseja enviar ações. 

  * Este dispositivo deve existir no arquivo hosts
  * Pode ser um grupo, um nome ou endereço específico.
  * Se você precisar especificar todos os hosts do arquivo, poderá usar o parâmetro "all".

* ``-m`` - especifica o módulo de execução.
* ``raw`` - parâmetro (módulo) de execução, este parâmetro deve ser seguido por algum comando à nível de usuário privilegiado independente de qual dispositivo de destino.
* ``-u teste`` - usuário remoto utilizado para estabelecer a conexão SSH. 
* ``-k`` - especifica a senha do usuário descrito no parâmetro anterior, a senha deve ser inserida após a execução do comando Ad-Hoc.

O resultado dessa execução será assim:

.. code:: bash

    thiago@thiago-ThinkPad:~/Documentos/Code/Ansible/lab1$ ansible SW_CORE_1 -m raw -a "show vlan brief" -u teste -k
    SSH password: 
    SW_CORE_1 | CHANGED | rc=0 >>


    VLAN Name                             Status    Ports
    ---- -------------------------------- --------- -------------------------------
    1    default                          active    Et0/0, Et0/1, Et0/2, Et0/3
                                                    Et1/0, Et1/1, Et1/2, Et1/3
                                                    Et2/0, Et2/1, Et2/2, Et2/3
    10   Vlan 10                          active    
    20   Vlan 20                          active    
    30   Vlan 30                          active    
    40   Vlan 40                          active    
    80   VLAN0080                         active    
    90   VLAN 90                          active    
    100  Vlan 100                         active    
    110  Vlan 110                         active    
    1002 fddi-default                     act/unsup 
    1003 token-ring-default               act/unsup 
    1004 fddinet-default                  act/unsup 
    1005 trnet-default                    act/unsup Shared connection to sw_core_1 closed.  

Tudo ocorreu bem e a saída do dispositivo foi exibida.

Iremos executar outros comandos e / ou em outras combinações de parâmetros.

Abaixo segue outro exemplo do Ad-Hoc em ação:

.. code:: bash

    $ ansible ansible_core -i ./hosts -m raw -a "show users" -u teste -k

Os valores acima irão executar o comando ``show users`` em todos os hosts do grupo ``ansible_core`` alocados dentro do arquivo ``./hosts`` e o parâmetro ``-a`` permite enviar argumentos para os dispositivos remotos.

O resultado dessa execução será assim:

.. code:: bash

    thiago@thiago-ThinkPad:~/Documentos/Code/Ansible/lab1$ ansible ansible_core -i ./hosts -m raw -a "show users" -u teste -k
    SSH password: 
    SW_CORE_1 | CHANGED | rc=0 >>
        Line       User       Host(s)              Idle       Location
    *  2 vty 0     teste      idle                 00:00:00 192.168.36.1

      Interface    User               Mode         Idle     Peer Address
    Shared connection to sw_core_1 closed.

    SW_CORE_2 | CHANGED | rc=0 >>

        Line       User       Host(s)              Idle       Location
    *  2 vty 0     teste      idle                 00:00:00 192.168.36.1

      Interface    User               Mode         Idle     Peer Address
    Shared connection to sw_core_2 closed.

Mais um exemplo do comando Ad-Hoc:

.. code:: bash

    $ ansible ansible_core -i ./hosts -m raw -a "show run" -u teste -k | grep 'hostname\|username' > usernames.txt

Acima, definimos que irá ser executado o comando ``show run`` em todos os devices do grupo ``ansible_core``, porém, desejamos que apenas as linhas ``'hostname\|username'`` sejam gravadas no txt ``> usernames.txt``.

O resultado dessa execução será assim:

.. code:: bash

    thiago@thiago-ThinkPad:~/Documentos/Code/Ansible/lab1$ cat usernames.txt 
    hostname SW_CORE_2
    username teste privilege 15 password 0 teste
    hostname SW_CORE_1
    username teste privilege 15 password 0 teste

Um exemplo muito além e que irá nos ajudar a fazer outras combinações para lidar com os comandos Ad-Hoc, segue exemplo do comando abaixo:

.. code:: bash

    $ ansible ansible_core -i hosts -c network_cli -e ansible_network_os=ios -u teste -k -m ios_config -a "commands='vlan 15'"
    
Vamos lidar com os principais parâmetros do comando:

* ``ansible_core`` - grupo ao qual você deseja enviar ações.
* ``-i hosts`` - arquivo hosts
* ``-c network_cli`` - a opção -c permite especificar o tipo de conexão. O tipo network_cli se refere ao protocolo SSH sobre CLI.
* ``-e ansible_network_os=ios`` - especifica o tipo de plataforma dos dispositivos do grupo ansbile_core.
* ``-m ios_config`` - este comando permite especificar o tipo do módulo a ser utilizado.
* ``"commands='vlan 15'"`` - comando a ser enviado para os dispositivos remotos.

E o resultado da execução permanecerá na running-config dos dispositivos.
