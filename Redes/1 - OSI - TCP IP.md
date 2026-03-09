### Camada OSI

O modelo OSI (Open Systems Interconnection) é um modelo de referência que divide a comunicação em redes em 7 camadas, cada uma com uma responsabilidade específica.

Dentro da camada OSI podemos definir ela pelas seguintes camadas:

```
1 - Infra - Transmissão de bits no meio físico - Cabos, Wi-Fi
2 - Enlace - Ethernet, MAC
3 - Rede - Endereçamento e roteamento - IP, ICMP
4 - Transporte - Entrega confiável, portas - TCP, UDP
5 - Sessão - Controla conexões e sessões - NetBIOS, RPC
6 - Apresentação - Tradução, criptografia, compressão - SSL/TLS, JPEG
7 - Aplicação - Interface com o usuário/software - HTTP, DNS, FTP
```

---
### C.I.D.R

CIDR (Classless Inter-Domain Routing) é uma forma de representar um bloco de endereços IP usando a notação IP/prefixo.

O número após a / diz quantos bits pertencem à rede — o resto é para os hosts (máquinas) dentro dela.

Exemplos práticos:

`192.168.1.0/24` — **rede doméstica típica**
IPs disponíveis: `192.168.1.1` até `192.168.1.254`
Total: 254 hosts
Usado em: redes Wi-Fi de casa, escritórios pequenos

`10.0.0.0/16` **— rede corporativa ou VPC na AWS**
IPs disponíveis: 10.0.0.1 até 10.0.255.254
Total: 65.534 hosts
Usado em: ambientes cloud, VPCs

`172.16.0.0/12` **— redes privadas médias**
Total: ~1 milhão de IPs
Usado em: data centers, redes internas grandes

`0.0.0.0/0` **— representa todos os IPs**
Usado em: rotas padrão, regras de firewall que liberam qualquer origem

`192.168.1.50/32` **— representa um único IP**
Usado em: liberar acesso apenas para uma máquina específica

---

### TCP & UDP

São os dois principais protocolos de transporte (Camada 4 do modelo OSI). Eles definem como os dados são enviados entre duas máquinas na rede.

**TCP — Transmission Control Protocol**

É o protocolo confiável. Antes de enviar dados, estabelece uma conexão e garante que tudo chegou corretamente.

Analogia: É como enviar uma carta com aviso de recebimento — você só sabe que foi entregue quando recebe a confirmação.

Como funciona — o famoso Three-Way Handshake:

```
Cliente  →  SYN        →  Servidor   (quero conectar)
Cliente  ←  SYN-ACK    ←  Servidor   (ok, pode vir)
Cliente  →  ACK        →  Servidor   (conectado!)
```

**UDP — User Datagram Protocol**

É o protocolo rápido. Envia os dados sem estabelecer conexão e sem verificar se chegaram.

Analogia: É como jogar um panfleto pela janela — você joga e não se preocupa se alguém pegou.

```
Cliente  →  Dados  →  Servidor   (sem confirmação, sem handshake)
```

**Regra geral:** se a aplicação não pode perder dados → **TCP**. Se velocidade importa mais que perfeição → **UDP**.

---

### Troubleshooting de Redes

`telnet` :  Ferramenta para testar conectividade TCP com um host em uma porta específica. Muito usado para verificar se um serviço está acessível antes de debugar a aplicação em si.

```
# Testar se a porta 80 está aberta
$ telnet google.com 80

# Testar conexão com banco de dados
$ telnet 10.0.1.50 5432

# Testar se o Redis está acessível
$ telnet localhost 6379
```

`Connected to...` → porta aberta, serviço acessível 
`Connection refused` → porta fechada ou serviço não está rodando 
`Connection timed out` → firewall bloqueando ou host inacessível 

`netstat` : Exibe conexões de rede ativas, portas em uso e estatísticas do sistema. Útil para descobrir o que está escutando em qual porta.

```
# Ver todas as portas em uso
$ netstat -tuln

# Ver portas com o processo que está usando
$ netstat -tulnp

# Ver conexões ativas no momento
$ netstat -an

# Filtrar por porta específica
$ netstat -tulnp | grep 8080

# Ver conexões estabelecidas
$ netstat -an | grep ESTABLISHED
```

`lsof` : List Open Files — lista todos os arquivos abertos pelo sistema, incluindo sockets de rede. No Linux, conexões de rede são tratadas como arquivos.

```
# Ver todos os processos usando rede
$ lsof -i

# Ver quem está usando a porta 8080
$ lsof -i :8080

# Ver conexões TCP estabelecidas
$ lsof -i TCP

# Ver arquivos abertos por um processo específico
$ lsof -p 1234

# Ver quem está usando uma porta e matar o processo
$ lsof -i :3000
$ kill -9 <PID>
```

Muito útil quando o `netstat` diz que uma porta está em uso mas você não sabe qual processo é.

`tcpdumb` : Captura pacotes de rede em tempo real diretamente na interface de rede. É o Wireshark do terminal — captura o tráfego bruto que passa pela máquina.

```
# Capturar todo tráfego da interface eth0
$ tcpdump -i eth0

# Capturar tráfego de um IP específico
$ tcpdump -i eth0 host 192.168.1.50

# Capturar tráfego de uma porta específica
$ tcpdump -i eth0 port 80

# Capturar e salvar em arquivo para analisar no Wireshark
$ tcpdump -i eth0 -w captura.pcap

# Capturar tráfego HTTP e mostrar conteúdo
$ tcpdump -i eth0 -A port 80

# Capturar tráfego entre dois hosts
$ tcpdump -i eth0 src 10.0.0.1 and dst 10.0.0.2
```

Requer permissão de root `sudo tcpdump`

`Wireshark` : Interface **gráfica** para captura e análise de pacotes de rede. Faz o mesmo que o `tcpdump` mas com visualização detalhada, filtros avançados e decodificação de protocolos.

**Casos de uso:**
- Analisar arquivos `.pcap` gerados pelo `tcpdump`
- Inspecionar handshake TCP/TLS visualmente
- Debugar protocolos HTTP, DNS, gRPC
- Analisar latência entre pacotes

```
# 1. Capturar no servidor (sem interface gráfica)
$ sudo tcpdump -i eth0 port 443 -w captura.pcap

# 2. Copiar o arquivo para sua máquina local
$ $cp usuario@servidor:/tmp/captura.pcap .

# 3. Abrir no Wireshark para análise visual
```


