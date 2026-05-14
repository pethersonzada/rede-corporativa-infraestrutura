# Rede Corporativa Segmentada com Cisco Packet Tracer

Projeto acadêmico de infraestrutura de rede corporativa com segmentação por VLANs, endereçamento VLSM e expansão wireless WPA2-AES, desenvolvido no Cisco Packet Tracer como parte da disciplina de Redes de Computadores da UNINASSAU.
Visão Geral

A rede atende seis departamentos de uma empresa fictícia, divididos em dois grupos: quatro setores cabeados com switches Cisco 2950-24 e VLANs configuradas, e dois setores wireless operando via roteadores HomeRouter-PT sem switch dedicado.
Tecnologias Utilizadas

    - VLANs em modo Access para isolamento de tráfego entre dispositivos do mesmo setor
    - Sub-redes /27 com VLSM e máscara 255.255.255.224
    - Wi-Fi WPA2-Personal com criptografia AES
    - DHCP automático nos segmentos wireless
    - Switches Cisco 2950-24 nos setores cabeados
    - Roteadores HomeRouter-PT nos setores wireless

## Topologia

<img width="747" height="389" alt="image" src="https://github.com/user-attachments/assets/4748f0a2-e232-4268-85a7-dcf2f6ae8b09" />

Identificação visual dos setores por cor:

* Verde: Engenharia
* Azul escuro: TI Interno
* Amarelo: Compras
* Azul petróleo: Infraestrutura
* Vermelho: Call Center
* Rosa: Diretoria

## Plano de Endereçamento

* Engenharia: 192.168.0.0/27 | Gateway: 192.168.0.1 | Hosts: .1 a .30
* Compras: 192.168.0.32/27 | Gateway: 192.168.0.33 | Hosts: .33 a .62
* TI Interno: 192.168.0.64/27 | Gateway: 192.168.0.65 | Hosts: .65 a .94
* Infraestrutura: 192.168.0.96/27 | Gateway: 192.168.0.97 | Hosts: .97 a .126
* Diretoria/Finanças (Wi-Fi): 192.168.0.128/27 | Gateway: 192.168.0.129 | Hosts: .129 a .158
* Call Center/Comercial (Wi-Fi): 192.168.0.160/27 | Gateway: 192.168.0.161 | Hosts: .161 a .190
* Segmentação por VLANs

Aplicada nos quatro switches dos setores cabeados. Cada switch divide suas 24 portas em dois domínios de broadcast isolados.

####  VLAN 1: portas Fa0/1 a Fa0/12, primeira metade do setor.
#### VLAN 2: portas Fa0/13 a Fa0/24, segunda metade do setor.

O isolamento impede comunicação direta entre VLANs sem roteamento explícito, validado por testes de ping.

## Configuração Wireless

### Roteador Wi-Fi 01 — Diretoria/Finanças
SSID: WIFI_CORPORATIVO_ALFA | Segurança: WPA2-Personal (AES) | Gateway: 192.168.0.129 | DHCP Start: 192.168.0.130

### Roteador Wi-Fi 02 — Call Center/Comercial
SSID: WIFI_OPERACIONAL_BETA | Segurança: WPA2-Personal (AES) | Gateway: 192.168.0.161 | DHCP Start: 192.168.0.162

## Testes Realizados

Ping entre dispositivos da mesma VLAN: sucesso.
Ping entre VLANs distintas: Destination host unreachable (comportamento esperado).
Ping de laptop ao gateway wireless: sucesso em ambos os segmentos.
Ping entre segmentos Wi-Fi diferentes: Destination host unreachable (isolamento confirmado).
Simulação PDU no modo Simulation: pacote entregue corretamente dentro do mesmo segmento.
