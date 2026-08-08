

Laboratório prático desenvolvido para simular uma arquitetura de rede corporativa utilizando o **Cisco Packet Tracer**. O projeto foca em segmentação de redes, segurança perimetral e roteamento dinâmico IP.

## 🛠️ Tecnologias e Protocolos Utilizados
* **Cisco IOS CLI:** Configuração manual de switches e roteadores.
* **VLANs (Virtual Local Area Networks):** Segmentação lógica das redes corporativas (VLAN 10 e VLAN 20).
* **IEEE 802.1Q (Trunking):** Configuração de porta Trunk para transporte multitáfego de dados.
* **OSPFv2 (Open Shortest Path First):** Ativação do protocolo de roteamento dinâmico utilizando máscaras curinga (*wildcard masks*).

================================================================ 


  
MEU GUIA RÁPIDO DE COMANDOS CISCO    (ROUTER-ON-A-STICK & OSPF) 


================================================================

1. NO SWITCH (Criar VLANs e definir acessos)
-------------------------------------------------------------------
conf t                      -> Entra no modo de configuração

vlan 10                     -> Cria a VLAN 10

name Nome                   -> Dá nome para a VLAN

int fa0/1                   -> Entra na porta do computador 1

sw mo ac                    -> Define a porta como modo acesso

sw ac vl 10                 -> Associa a porta à VLAN 10

int g0/1                    -> Entra na porta que vai para o roteador

sw mo tr                    -> Transforma a porta em TRUNK (passa tudo)

show vlan brief             -> COMANDO DE TESTE: Mostra as VLANs ativas


2. NO ROTEADOR (Dividir a porta em sub-interfaces e ligar o OSPF)
-------------------------------------------------------------------
int g0/0                    -> Entra na porta física principal

no shut                     -> LIGA a porta física (bolinha fica verde)

int g0/0.10                 -> Cria a sub-interface para a VLAN 10

encapsulation dot1Q 10      -> Ativa o protocolo de Tag de VLAN 10

ip address 192.168.10.1 255.255.255.0 -> Define o Gateway da rede

router ospf 1               -> Liga o protocolo de roteamento OSPF

network 192.168.10.0 0.0.0.255 area 0 -> Avisa ao OSPF que essa rede existe

show ip route               -> COMANDO DE TESTE: Mostra as IP Tables (Tabela de rotas)
