# Aula 2 — Administração de Usuários, Grupos e Permissões no Linux

**Aluno:** Elioenai Adalberto Silva Santos  
**Instituição:** Instituto Federal de Alagoas — IFAL  
**Disciplina:** Laboratório de Sistemas Operacionais e Redes

## 1. Objetivo

Praticar a administração de usuários, grupos e permissões no Ubuntu Server, utilizando comandos do terminal Linux para controlar o acesso a arquivos e diretórios.

## 2. Desenvolvimento das atividades

### 2.1. Criação de usuários

Foram utilizados comandos para criar usuários no Ubuntu Server.

```bash
sudo adduser fulano
sudo adduser cicrano
sudo adduser beltrano
sudo adduser novato
```

Esses comandos permitem criar contas de usuários no sistema.

**Evidências:**

![Criação do usuário Fulano](imagens/aula2_criacao_fulano.png)

![Criação do usuário Cicrano](imagens/aula2_criacao_cicrano.png)

![Criação do usuário Beltrano](imagens/aula2_criacao_beltrano.png)

![Criação do usuário Novato](imagens/aula2_criacao_novato.png)

### 2.2. Verificação dos usuários cadastrados

Foi utilizado o arquivo `/etc/passwd` para consultar informações sobre os usuários cadastrados no Linux.

```bash
cat /etc/passwd
```

**Evidência:**

![Verificação dos usuários](imagens/aula2_usuarios_passwd.png)

### 2.3. Criação do grupo devs

Foi realizada a configuração de um grupo denominado `devs`, destinado à organização de usuários e ao gerenciamento de permissões.

```bash
sudo groupadd devs
```

Para adicionar usuários ao grupo, foi utilizado o comando `usermod`.

```bash
sudo usermod -aG devs fulano
sudo usermod -aG devs cicrano
sudo usermod -aG devs beltrano
```

A opção `-aG` permite adicionar um usuário a um grupo suplementar sem remover os demais grupos dos quais ele participa.

**Evidências:**

![Configuração do grupo devs](imagens/aula2_grupo_devs.png)

![Verificação do grupo devs](imagens/aula2_grupo_devs_verificacao.png)

### 2.4. Configuração do diretório projeto

Foi utilizado o diretório `/srv/projeto` para praticar o gerenciamento de permissões.

```bash
sudo mkdir -p /srv/projeto
```

O grupo `devs` foi associado ao diretório, permitindo controlar o acesso dos usuários integrantes desse grupo.

Foi utilizada a permissão `770`:

```bash
sudo chmod 770 /srv/projeto
```

Essa permissão representa:

- Proprietário: leitura, escrita e execução.
- Grupo: leitura, escrita e execução.
- Outros usuários: nenhuma permissão.

**Evidências:**

![Permissões do projeto](imagens/aula2_permissoes_projeto.png)

![Verificação das permissões](imagens/aula2_permissoes_projeto_2.png)

### 2.5. Teste de acesso ao diretório

Foram realizados testes de acesso com usuários cadastrados no sistema para observar o comportamento das permissões configuradas.

**Evidência:**

![Teste de acesso com Fulano](imagens/aula2_teste_acesso_fulano.png)

### 2.6. Criação e configuração do grupo financeiro

Também foram realizados procedimentos de gerenciamento de um grupo denominado `financeiro`.

A atividade envolveu a configuração do diretório `/srv/financeiro` e a definição das permissões de acesso.

Foi utilizada a permissão `2770`:

```bash
sudo chmod 2770 /srv/financeiro
```

O número `2` inicial ativa o bit SGID, que faz com que novos arquivos e subdiretórios criados nesse diretório herdem seu grupo, nas condições normais de criação.

**Evidências:**

![Grupo financeiro](imagens/aula2_grupo_financeiro.png)

![Configuração do grupo financeiro](imagens/aula2_grupo_financeiro_2.png)

![Permissões do diretório financeiro](imagens/aula2_permissoes_financeiro.png)

### 2.7. Testes com diferentes usuários

Foram realizados testes utilizando os usuários Cicrano e Novato, com o objetivo de observar as restrições e permissões aplicadas aos diretórios.

**Evidências:**

![Teste com Cicrano](imagens/aula2_teste_cicrano.png)

![Teste com Novato](imagens/aula2_teste_novato.png)

![Segundo teste com Novato](imagens/aula2_teste_novato_2.png)

### 2.8. Testes de manipulação de arquivos

Foram realizados procedimentos de criação, escrita e leitura de arquivos por meio do terminal.

Durante um dos testes de leitura, foi apresentada uma mensagem de arquivo não encontrado para o nome informado. Portanto, esse teste não foi considerado uma leitura concluída com sucesso.

**Evidências:**

![Teste de arquivo](imagens/aula2_teste_arquivo.png)

![Segundo teste de arquivo](imagens/aula2_teste_arquivo_2.png)

## 3. Conclusão

A atividade permitiu compreender melhor o funcionamento do gerenciamento de usuários, grupos e permissões no Ubuntu Server.

Foram praticados comandos de criação de usuários, organização de grupos, configuração de permissões e testes de acesso a diretórios e arquivos.

Os procedimentos demonstraram a importância das permissões para a organização e a segurança de um sistema Linux.
