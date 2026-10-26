# Redes3

# Aula 03 — Interfaces e Endereçamento de Rede

## 1. Identificação

- **Aluno:** Elioenai Adalberto Silva Santos
- **Instituição:** IFAL — Campus Maceió
- **Curso:** Desenvolvimento de Sistemas
- **Turma:** 912-A
- **Data:** 26/10/2026
- **Atividade:** Laboratório de Redes — Aula 03

## 2. Objetivo

Identificar e analisar as interfaces de rede e as configurações de endereçamento IP do Ubuntu Server, consultar a tabela de rotas, testar a conectividade utilizando o comando `ping`, rastrear o caminho dos pacotes com `traceroute` e comparar os modos NAT e Placa em Ponte (Bridge) do VirtualBox com a configuração de rede do Windows.

## 3. Ambiente utilizado

- **Sistema operacional da máquina virtual:** Ubuntu Server 22.04.5 LTS
- **Virtualizador:** Oracle VirtualBox
- **Interface de rede da VM:** `enp0s3`
- **Sistema operacional hospedeiro:** Windows

### 3.1. Configuração da máquina virtual em NAT

| Informação | Resultado |
|---|---|
| Interface de rede | `enp0s3` |
| Endereço IPv4 | `10.0.2.15` |
| Prefixo | `/24` |
| Máscara de sub-rede | `255.255.255.0` |
| Endereço MAC | `08:00:27:51:02:bc` |
| Gateway padrão | `10.0.2.2` |

### 3.2. Configuração da máquina virtual em Bridge

| Informação | Resultado |
|---|---|
| Interface de rede | `enp0s3` |
| Endereço IPv4 | `172.20.20.244` |
| Prefixo | `/22` |
| Máscara de sub-rede | `255.255.252.0` |
| Endereço MAC | `08:00:27:51:02:bc` |
| Gateway padrão | `172.20.20.1` |

### 3.3. Configuração do Windows

Os dados foram obtidos por meio do comando `ipconfig /all`.

| Informação | Resultado |
|---|---|
| Endereço IPv4 | `172.20.20.232` |
| Máscara de sub-rede | `255.255.252.0` |
| Prefixo | `/22` |
| Gateway padrão | `172.20.20.1` |
| Endereço MAC | `60:C7:27:32:79:00` |

## 4. Procedimentos realizados

### 4.1. Inspeção das interfaces de rede

Foi utilizado o comando:

```bash
ip addr show
```

Esse comando permitiu identificar as interfaces de rede, os endereços IPv4, os prefixos e os endereços MAC. A interface `enp0s3` foi identificada como a interface de rede principal da máquina virtual.

### 4.2. Verificação do estado das interfaces

Foi utilizado o comando:

```bash
ip link
```

O comando permite verificar o estado das interfaces de rede e consultar seus endereços MAC.

### 4.3. Consulta da tabela de rotas

Foi utilizado o comando:

```bash
ip route
```

A consulta permitiu identificar a rota padrão e o gateway utilizado pela máquina virtual em cada modo de rede.

No modo NAT, o gateway identificado foi `10.0.2.2`. No modo Bridge, o gateway identificado foi `172.20.20.1`.

### 4.4. Verificação do Netplan

Foi tentado executar o comando:

```bash
netplan status
```

Entretanto, o comando apresentou erro nessa instalação. Por esse motivo, as informações de endereçamento e roteamento foram obtidas principalmente por meio dos comandos `ip addr show`, `ip link` e `ip route`.

### 4.5. Testes de conectividade

Foram realizados testes com o comando `ping` para verificar a comunicação com o gateway, o acesso a um endereço IP externo e a resolução de nomes DNS.

Os comandos utilizados foram:

```bash
ping -c 4 10.0.2.2
```

```bash
ping -c 4 8.8.8.8
```

```bash
ping -c 4 google.com
```

Os testes foram realizados e o usuário confirmou que os testes de ping foram concluídos com sucesso.

### 4.6. Rastreamento de rotas

Foi utilizado o utilitário `traceroute` para investigar o caminho percorrido pelos pacotes até um destino externo.

Comando utilizado:

```bash
traceroute 8.8.8.8
```

O rastreamento permite observar os saltos intermediários entre a máquina virtual e o destino. Alguns dispositivos podem não responder às sondagens, o que pode ser indicado por asteriscos (`*`).

### 4.7. Alteração do modo de rede

A máquina virtual foi desligada para permitir a alteração do adaptador de rede nas configurações do VirtualBox.

Primeiramente, foi utilizado o modo NAT. Em seguida, o adaptador foi alterado para Placa em Ponte (Bridge), permitindo comparar os endereços IP, os gateways e a conectividade nos dois modos.

### 4.8. Consulta das configurações do Windows

No Windows, foi executado o comando:

```powershell
ipconfig /all
```

Esse comando permitiu consultar o endereço IPv4, a máscara de sub-rede, o gateway padrão e o endereço MAC do adaptador de rede utilizado pelo computador hospedeiro.

## 5. Testes e comparações
## Prints

![Print 1](Captura%20de%20tela%202026-10-26%20103918.png)

![Print 2](Captura%20de%20tela%202026-10-26%20103951.png)

![Print 3](Captura%20de%20tela%202026-10-26%20104839.png)

![Print 4](Captura%20de%20tela%202026-10-26%20105045.png)

![Print 5](Captura%20de%20tela%202026-10-26%20105121.png)

![Print 6](Captura%20de%20tela%202026-10-26%20105157.png)

![Print 7](Captura%20de%20tela%202026-10-26%20105219.png)

![Print 8](Captura%20de%20tela%202026-10-26%20105551.png)

![Print 9](Captura%20de%20tela%202026-10-26%20105610.png)

![Print 10](Captura%20de%20tela%202026-10-26%20105637.png)

![Print 11](Captura%20de%20tela%202026-10-26%20105934.png)
### 5.1. Comparação entre NAT, Bridge e Windows

| Característica | Ubuntu — NAT | Ubuntu — Bridge | Windows |
|---|---|---|---|
| Endereço IPv4 | `10.0.2.15` | `172.20.20.244` | `172.20.20.232` |
| Máscara | `255.255.255.0` | `255.255.252.0` | `255.255.252.0` |
| Prefixo | `/24` | `/22` | `/22` |
| Gateway padrão | `10.0.2.2` | `172.20.20.1` | `172.20.20.1` |
| Endereço MAC | `08:00:27:51:02:bc` | `08:00:27:51:02:bc` | `60:C7:27:32:79:00` |

### 5.2. Análise do modo NAT

No modo NAT, a máquina virtual recebeu o endereço IPv4 `10.0.2.15/24` e utilizou o gateway `10.0.2.2`.

Nesse modo, o VirtualBox realiza a tradução de endereços de rede para permitir que a máquina virtual acesse redes externas por meio da conexão do computador hospedeiro. O acesso direto do hospedeiro à máquina virtual pode exigir configurações adicionais, como redirecionamento de portas.

### 5.3. Análise do modo Bridge

No modo Bridge, a máquina virtual recebeu o endereço IPv4 `172.20.20.244/22`, utilizando o gateway `172.20.20.1`.

O computador hospedeiro apresentou o endereço IPv4 `172.20.20.232/22` e utilizou o mesmo gateway. Isso demonstra que a máquina virtual e o Windows estão na mesma sub-rede IPv4.

Nesse modo, a máquina virtual participa diretamente da rede local, podendo se comunicar com outros dispositivos, desde que as regras de firewall e as políticas da rede permitam.

### 5.4. Comparação dos endereços MAC

O endereço MAC identificado na interface virtual `enp0s3` foi `08:00:27:51:02:bc` tanto no NAT quanto no Bridge. Já o Windows apresentou o endereço MAC `60:C7:27:32:79:00`.

A manutenção do mesmo endereço MAC nos dois modos é compatível com a utilização da mesma placa de rede virtual, cuja configuração de endereço MAC não precisou ser alterada durante a prática.

### 5.5. Análise dos testes de conectividade

Os testes de `ping` foram concluídos com sucesso, conforme informado durante a execução da atividade.

O teste com o gateway verifica a comunicação com o próximo salto da rede. O teste com `8.8.8.8` verifica a conectividade com um destino externo por endereço IP. Já o teste com `google.com` permite verificar também se a resolução DNS está funcionando.

O `traceroute` complementa os testes ao apresentar os saltos intermediários do caminho até o destino.

## 6. Problemas encontrados e soluções

Durante a prática, o comando `netplan status` apresentou erro. Para continuar a análise, foram utilizados os comandos `ip addr show`, `ip link` e `ip route`, que forneceram as informações necessárias sobre as interfaces, os endereços IP e as rotas.

A comparação entre os modos NAT e Bridge foi realizada alterando a configuração do adaptador de rede no VirtualBox e verificando novamente os dados da máquina virtual.

Os resultados foram registrados por meio de capturas de tela dos comandos e testes realizados.

## 7. Conclusão

A atividade permitiu compreender como identificar interfaces de rede, endereços IPv4, prefixos, máscaras de sub-rede, endereços MAC e gateways padrão no Ubuntu Server e no Windows.

A comparação demonstrou que, no modo NAT, a máquina virtual utiliza uma rede virtual administrada pelo VirtualBox, enquanto, no modo Bridge, recebe um endereço pertencente à mesma sub-rede do computador hospedeiro.

Os testes de conectividade e o rastreamento de rotas complementaram a análise do funcionamento da rede. Dessa forma, a prática contribuiu para a compreensão do endereçamento IPv4, do roteamento, da conectividade e das diferenças entre os modos de rede disponíveis no VirtualBox.

## Evidências da prática

As capturas de tela dos comandos e dos testes realizados devem acompanhar este relatório, organizadas de forma que seja possível identificar cada etapa da atividade.
