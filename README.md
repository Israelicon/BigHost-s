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

