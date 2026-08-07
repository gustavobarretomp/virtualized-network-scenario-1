# Implementação no VirtualBox

Esta pasta reúne as evidências da implementação do Cenário 01 utilizando máquinas virtuais Ubuntu Server, redes internas do VirtualBox, FRRouting, BIND9 e Apache2.

## Testes dos clientes

### PC-A — conectividade com o WEB1

O teste confirma a comunicação entre o PC-A, localizado na LAN4, e o WEB1, localizado na LAN1.

![Ping do PC-A para o WEB1](clients/pc-a-ping-web1-corrigido.png)

### PC-A — acesso HTTP ao WEB1

![Acesso HTTP do PC-A ao WEB1](clients/pc-a-http-web1-corrigido.png)

### PC-C — conectividade com o WEB3

![Ping do PC-C para o WEB3](clients/pc-c-ping-web3-corrigido.png)

### PC-C — acesso HTTP ao WEB3

![Acesso HTTP do PC-C ao WEB3](clients/pc-c-http-web3-corrigido.png)

## Testes de roteamento

### Tabela de rotas do R1

A tabela mostra as redes diretamente conectadas e as rotas aprendidas dinamicamente pelo protocolo RIPv2.

![Tabela de rotas do R1](routers/r1-show-ip-route.png)

### Rotas RIPv2 do R1

![Rotas RIP do R1](routers/r1-show-ip-rip.png)

### Tabela de rotas do R5

![Tabela de rotas do R5](routers/r5-show-ip-route-corrigido.png)

## Testes dos servidores DNS

### Resolução pelo DNS1

O DNS1, no endereço `192.168.1.5`, resolveu os domínios `servidor1.rede.local` e `servidor2.rede.local`.

![Teste do DNS1](servers/dns1-nslookup-servidor1-e-2-ajustado.png)

### Resolução pelo DNS2

O DNS2, no endereço `192.168.4.5`, resolveu o domínio `servidor3.rede.local`.

![Teste do DNS2](servers/dns2-nslookup-servidor3-corrigido.png)

## Testes dos servidores Apache2

### WEB1

![Teste do Apache2 no WEB1](servers/web1-apache-test-corrigido.png)

### WEB2

![Teste do Apache2 no WEB2](servers/web2-apache-test-corrigido.png)

### WEB3

![Teste do Apache2 no WEB3](servers/web3-apache-test-corrigido.png)

## Resultado

Os testes comprovaram:

- funcionamento do roteamento dinâmico RIPv2;
- comunicação entre diferentes redes locais;
- resolução de nomes pelos servidores DNS;
- funcionamento dos três servidores Apache2;
- acesso aos serviços HTTP pelos clientes.
