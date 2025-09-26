# Nginx
Um servidor web capaz de atender vários clientes por meio de um pequeno grupo de processos.
O processos principal é o master, ele é responsável por ler os arquivo de configuração, criar o socket principal na porta definida pelo arquivo de configuração "nginx.conf", e então criar e gerenciar os workers.
Os workers são os processos responsáveis por lidar com as requisições dos clientes de forma assincrona e não bloqueante, por meio de eventos para cada uma delas.
Cada workder vai receber uma cópia do file descriptor do socket criado pelo processo master, e cada worker fica esperando pela notificação do kernel para aceitar uma nova conexão, ao aceitar, ele registra que a conexão está pronta para leitura, e quando novos dados dela chegam, o worker é notificado e ele processa a requisição.
O kernel é responsável permitir a atribuir a nova conexão que worker irá lidar, além de notificiar de novos dados daquela conexão específica, e a partir disso só esse worker fica responsável por processar as requisições http daquela conexão.

O serviço do servidor nginx é configurado por meio de arquivos de configurações no diretório "/etc/nginx/", o arquivo princiapal é: "nginx.conf" e nele você configura o servidor por meio de parâmetros simples como:

server {
  listen 80; # porta onde o servidor http atenderá
  server_name localhost; # ou www.meusite.com
}

Veja a documentação para mais detalhes.

Não alteramos o arquivo nginx.conf para exibir o site diretamente, na verdade alteramos ele para incluir um arquivo de configuração de servidor para nosso site específico. Exemplo de passo a passo:
Criar arquivo "site.conf" no diretório "sites-available" dentro de "/etc/nginx".

criar link simbolico para ele em sites-enabled (é realmente necessário passar os caminhos absolutos):
ln -s /etc/nginx/sites-available/site.conf /etc/nginx/sites-enabled/site.conf

Após isso é necessário incluir o arquivo de configuração do site no nginx.conf:
include /etc/nginx/sites-enabled/*;

Após isso é necessário recarregar o arquivo de configuração do serviço nginx "nginx.conf":
nginx -t

E então recarregar o serviço nginx, ou reiniciar o serviço por completo:
nginx -s reload
Ou utilizar o gerenciador de serviços para reiniciar o serviço nginx:
rc-service nginx restart

utiliza arquivos 
Ele pode agir como:
Proxy direto: Receber as requisições (dados http) dos clientes, e direcionar elas para a internet.
Proxy reverso: Onde irá receber as requisições (dados http) dos clientes, e direcionar eles para o servidor da aplicação em si.
