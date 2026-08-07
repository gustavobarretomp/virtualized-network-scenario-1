# Implementação no VirtualBox

Esta pasta reúne evidências da implementação do **Cenário 01** utilizando máquinas virtuais Ubuntu Server no Oracle VirtualBox.

Foram utilizados:

- redes internas do VirtualBox;
- FRRouting com RIPv2;
- BIND9 para resolução DNS;
- Apache2 para hospedagem das páginas;
- clientes Ubuntu Server para validação dos serviços.

---

## Testes dos clientes

### PC-A — ping para o WEB1

O PC-A conseguiu alcançar o WEB1, localizado no endereço `192.168.1.10`.

<p align="center">
  <img src="clients/pc-a-ping-web1.png" alt="Ping do PC-A para o WEB1" width="100%">
</p>

### PC-A — acesso HTTP ao WEB1

O comando `curl` confirmou o acesso à página hospedada pelo Apache2 no WEB1.

<p align="center">
  <img src="clients/pc-a-http-web1.png" alt="Acesso HTTP do PC-A ao WEB1" width="100%">
</p>

### PC-C — ping para o WEB3

O PC-C conseguiu alcançar o WEB3, localizado no endereço `192.168.3.10`.

<p align="center">
  <img src="clients/pc-c-ping-web3.png" alt="Ping do PC-C para o WEB3" width="100%">
</p>

### PC-C — acesso HTTP ao WEB3

O comando `curl` confirmou o acesso à página hospedada pelo Apache2 no WEB3.

<p align="center">
  <img src="clients/pc-c-http-web3.png" alt="Acesso HTTP do PC-C ao WEB3" width="100%">
</p>

---

## Testes de roteamento

### Tabela de rotas do R1

A tabela mostra as redes diretamente conectadas e as rotas aprendidas dinamicamente pelo protocolo RIPv2.

<p align="center">
  <img src="routers/r1-show-ip-route.png" alt="Tabela de rotas do R1" width="100%">
</p>

### Rotas RIPv2 do R1

O teste mostra as redes conhecidas pelo R1 e os próximos saltos utilizados para alcançar as redes remotas.

<p align="center">
  <img src="routers/r1-show-ip-rip.png" alt="Rotas RIPv2 do R1" width="100%">
</p>

### Tabela de rotas do R5

O R5 também aprendeu as redes remotas pelo protocolo RIPv2.

<p align="center">
  <img src="routers/r5-show-ip-route-.png" alt="Tabela de rotas do R5" width="100%">
</p>

---

## Testes dos servidores DNS

### Resolução pelo DNS1

O DNS1, localizado no endereço `192.168.1.5`, resolveu corretamente:

- `servidor1.rede.local` para `192.168.1.10`;
- `servidor2.rede.local` para `192.168.2.10`.

<p align="center">
  <img src="servers/dns1-nslookup-servidor1-e-2.png" alt="Teste de resolução do DNS1" width="100%">
</p>

### Resolução pelo DNS2

O DNS2, localizado no endereço `192.168.4.5`, resolveu corretamente:

- `servidor3.rede.local` para `192.168.3.10`.

<p align="center">
  <img src="servers/dns2-nslookup-servidor3.png" alt="Teste de resolução do DNS2" width="100%">
</p>

---

## Testes dos servidores Apache2

### WEB1

O serviço Apache2 está ativo no WEB1, no endereço `192.168.1.10`.

<p align="center">
  <img src="servers/web1-apache-test.png" alt="Teste do Apache2 no WEB1" width="100%">
</p>

### WEB2

O serviço Apache2 está ativo no WEB2, no endereço `192.168.2.10`.

<p align="center">
  <img src="servers/web2-apache-test.png" alt="Teste do Apache2 no WEB2" width="100%">
</p>

### WEB3

O serviço Apache2 está ativo no WEB3, no endereço `192.168.3.10`.

<p align="center">
  <img src="servers/web3-apache-test.png" alt="Teste do Apache2 no WEB3" width="100%">
</p>

---

## Configurações utilizadas

As configurações das máquinas estão disponíveis nas seguintes pastas:

- [Configurações dos clientes](../configs/clients/)
- [Configurações dos roteadores](../configs/routers/)
- [Configurações dos servidores DNS](../configs/dns/)
- [Configurações dos servidores web](../configs/web/)

---

## Resultado

Os testes comprovaram:

- funcionamento do roteamento dinâmico RIPv2;
- aprendizagem de rotas entre os cinco roteadores;
- comunicação entre redes diferentes;
- resolução dos nomes da zona `rede.local`;
- funcionamento dos servidores BIND9;
- funcionamento dos três servidores Apache2;
- acesso HTTP entre clientes e servidores de redes distintas.
