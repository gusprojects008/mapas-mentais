# O que é D-Bus? e como funciona?

No linux, o D-Bus (Desktop Bus) é um barramento de comunicação IPC (Inter processes comunication), ou seja, usado para comunicação entre processos no linux. Ele é um componente essencial usado por aplicações que dependem de outros serviços ou deamons que estão sendo executado no sistema, para chamar metódos, enviar sinais, comunicar processos sem precisar criar protocolos TCṔ/Unix manualmente.

Existem 2 tipos de B-Bus:

- System D-Bus: Usado para comunicação entre serviços e deamons do sistema e user-space, como: NetworkManager, BlueZ, UPower, systemd-elogind etc... Exemplo: Aplicação gráfica de gerenciamento de conexões de rede wireless, chama métodos do NetworkManager como: (org.freedesktop.NetworkManager.GetDevices()) para obter e listar os dispositivos de rede disponíveis, e então faz a exibição das informações na janela do aplicativo.

- Session D-Bus: Usado para comunicação entre serviços e processos em espaço de usuário (user-mode), ele é um barramento de comunicação IPC por sessão de usuário, ou seja, cada sessão de login de usuário do sistema pode ter sua própria sessão D-Bus.
