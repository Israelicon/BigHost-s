## BigHost-s
![bandicam 2024-11-06 05-52-10-858](https://github.com/user-attachments/assets/f641b7e9-18eb-4ea1-ada1-18cd423b1fbe)

A Sala BigHost-s trata-se de uma sala que tem um servidor web vulnerável, mais pra frente eu falo a falha.

pra explorar vamos apertar em Start Machine para começar a explorar a máquina
![bandicam 2024-11-06 05-51-43-911](https://github.com/user-attachments/assets/a6f82900-8f5d-46ca-81e2-dd1efa617bbd)

após receber um IP, vamos pingar ele para verificar se está conectado e acessível na rede Isso ajuda a determinar:

- Se o dispositivo está online: Se o dispositivo responde ao ping, ele está conectado e acessível.
- A qualidade da conexão: O tempo de resposta mostra a latência, ou seja, o quão rápido o dispositivo responde ao pedido de ping.

vamos usar o ping no próprio terminal
![bandicam 2024-11-06 05-52-57-973](https://github.com/user-attachments/assets/402e63f7-dccc-4ae3-bacf-924e91e2ecbf)

após isso podemos explorar quais serviços estao rodando na máquina, pra isso precisamos de um portscan, um portscan bem famoso é o Nmap, só com o nmap e o ip ele pode mostrar pra gente qual porta está
aberta e até a versão do serviço que está rodando, mas nesse caso usaremos <nmap 10.10.29.148>
![bandicam 2024-11-06 05-53-47-126](https://github.com/user-attachments/assets/3c968772-d61c-4ca6-b3f0-911e65049363)

o nmap escaneou, e deu o resultado que duas portas estão abertas, ssh e http

- ssh: é um protocolo seguro que permite acessar e gerenciar dispositivos remotamente através de uma rede. Ele é amplamente utilizado para administrar servidores e computadores de maneira segura, localizada na porta 22

- http: é um protocolo usado para transferir páginas web e outros tipos de dados através da internet. Ele é o protocolo base para a navegação na web. Diferente do SSH, o HTTP não tem criptografia por padrão

podemos colocar o ip no navegador pra ver a pagina do servidor web
![bandicam 2024-11-06 05-54-32-214](https://github.com/user-attachments/assets/fd249904-9fc0-43c4-9092-61ba16c50a7d)

parece um site pra compra de domínio e hosts, podemos explorar os diretórios pra ver onde tem arquivos ou páginas secretas, podemos usar um bruteforce de diretórios chamado Gobuster, usamos url e 
caminho da wordlists 
![bandicam 2024-11-06 05-57-55-127](https://github.com/user-attachments/assets/15c94c57-cfe9-4441-98a4-e78aa88ea307)

ele achou index.php e info.php, o info.php pode ser útil quando encontramos uma página vulneravel a LFI

navegando na página podemos ver um diretório chamado "Contat Us"
![bandicam 2024-11-06 05-58-57-382](https://github.com/user-attachments/assets/398c16bf-5e10-4b12-abca-da81cfcd3e05)

é nele onde podemos testar a falha de LFI, Local File Inclusion
- LFI (Local File Inclusion) é uma vulnerabilidade comum em aplicativos web, que permite a um invasor incluir e acessar arquivos do próprio servidor da aplicação. Essa falha ocorre quando um aplicativo permite que o usuário especifique o caminho de um arquivo sem uma validação adequada, permitindo que o invasor inclua arquivos locais do servidor.

Imagine que um site tenha uma URL como esta:

- http://exemplo.com/index.php?page=home.php

Se o aplicativo não filtra adequadamente o valor do parâmetro page, um invasor pode manipulá-lo para tentar incluir arquivos locais, como:

- http://exemplo.com/index.php?page=/etc/passwd

Se o servidor for vulnerável, o arquivo /etc/passwd (em sistemas Linux) será exibido, revelando informações sobre os usuários do sistema, como nesse caso aqui:
![bandicam 2024-11-06 05-59-35-939](https://github.com/user-attachments/assets/aa96c5f6-8532-4ce1-8fb9-ea959e796c8c)

podemos perceber que existe um usuario chamado john, podemos testar quebrar a senha pra testar na porta 22, que é o ssh, caso quebrado podemos logar no ssh do sistema

pra testar, podemos usar o hydra, um ferramenta de bruteforce de senhas, como nesse exemplo
![bandicam 2024-11-06 06-04-25-241](https://github.com/user-attachments/assets/58ec5297-ebda-460b-bb0c-bf14041fef79)

descobrimos que a senha é john, agora com a senha em mãos, vamos logar no ssh, pra logar no ssh é simples bastar colocar esse comando no terminal

- ssh john@10.10.29.148

após isso coloque a senha e pronto, voce já está dentro do ssh
![bandicam 2024-11-06 06-06-41-478](https://github.com/user-attachments/assets/3350e8b1-4dbd-4ebf-97c5-9086ac4f85df)

após isso, vamos procurar o arquivo user.txt para responder as questões do tryhackme, procurei e achei botando o comando cd /, para entrar na raíz do servidor
![bandicam 2024-11-06 06-08-07-958](https://github.com/user-attachments/assets/2b5617ee-b92b-43bd-a442-020fd481cec4)

conseguimos achar, agora é a hora de escalar privilégios na máquina, pra pegar o root.txt, pois não temos permissão pra entrar no /root, tentei usar o sudo -l e percebi que não precisamos pegar info 
pra escalar, só um sudo su, ele já coloca o usuario como root

![bandicam 2024-11-06 06-09-01-643](https://github.com/user-attachments/assets/767b1e21-d1d8-4887-8634-b92d44d7f83a)


agora que conseguimos, é só responder a segunda pergunta e terminamos a máquina.

