# desafio-dio-azure-recursos-dimensionamentos-maquinasvirtuais
Repositório criado para o Desafio da DIO (Digital Innovation One) sobre Recursos e Dimensionamentos em Máquinas Virtuais no Microsoft Azure.
Contém um guia passo a passo em Markdown que ensina como criar, configurar e dimensionar uma VM (Máquina Virtual) no portal do Azure, incluindo boas práticas para otimização de custo e desempenho.
Ideal para quem está iniciando no Azure e deseja entender como provisionar recursos de forma prática e objetiva.

# Recursos e Dimensionamentos em Máquinas Virtuais na Azure

## Índice
1. [Acessando o serviço de Máquinas Virtuais](#1-acessando-o-serviço-de-máquinas-virtuais)
2. [Selecionando configurações pré-definidas](#2-selecionando-configurações-pré-definidas)
3. [Escolhendo o tipo de carga de trabalho](#3-escolhendo-o-tipo-de-carga-de-trabalho)
4. [Configurando opções avançadas](#4-configurando-opções-avançadas)
5. [Selecionando o tamanho da VM](#5-selecionando-o-tamanho-da-vm)
6. [Configurando rede e segurança](#6-configurando-rede-e-segurança)
7. [Discos e armazenamento](#7-discos-e-armazenamento)
8. [Criando a VM](#8-criando-a-vm)

---

## 1. Acessando o serviço de Máquinas Virtuais

1. No portal Azure, navegue até **Todos os serviços** > **Computação** > **Máquinas Virtuais**
2. Clique em **Criar** e selecione **Máquina virtual do Azure**

## 2. Selecionando configurações pré-definidas

Azure oferece configurações pré-definidas baseadas em cargas de trabalho:

- **Desenvolvimento/Teste**
  - Diagnóstico de inicialização
  - Alta disponibilidade (opcional)
  - Backup do Azure (quando disponível)

- **Produção**
  - Configurações padrão otimizadas
  - Alta disponibilidade recomendada
  - Backup automático

## 3. Escolhendo o tipo de carga de trabalho

Selecione o tipo que melhor atende sua necessidade:

| Tipo de Carga | Série Recomendada | Casos de Uso | Exemplo de Tamanhos |
|--------------|------------------|-------------|---------------------|
| Uso geral | Série D | Aplicativos empresariais, bancos de dados | DS2_v2: 2 CPU, 7 GB<br>DS3_v2: 4 CPU, 14 GB |
| Otimizado para memória | Série E | SAP HANA, SQL Hekaton | E2s_v3: 2 CPU, 16 GB<br>E4s_v3: 4 CPU, 32 GB |
| Computação otimizada | Série F | Processamento em lotes, servidores Web | F2s_v2: 2 CPU, 4 GB<br>F4s_v2: 4 CPU, 8 GB |

## 4. Configurando opções avançadas

### Instâncias Spot
- Oferecem capacidade não utilizada com desconto
- Ideal para cargas tolerantes a interrupções
- Podem ser interrompidas se a capacidade for necessária para VMs regulares

### Hibernação (Visualização)
- Requer registro da assinatura
- Permite salvar o estado da VM quando desligada

## 5. Selecionando o tamanho da VM

1. Na seção **Tamanho**, clique em **Ver todos os tamanhos**
2. Filtre por:
   - Número de vCPUs
   - Quantidade de RAM
   - Tipo de carga de trabalho
3. Considere:
   - Custo mensal estimado
   - Compatibilidade com discos Ultra (se necessário)

## 6. Configurando rede e segurança

### Portas de entrada
- Selecione apenas as necessárias:
  - RDP (3389) para Windows
  - SSH (22) para Linux
  - HTTP (80) e HTTPS (443) para servidores web

### Benefício Híbrido do Azure
- Economize até 49% usando licenças existentes do Windows Server

## 7. Discos e armazenamento

### Disco do SO
- SSD Premium recomendado para produção
- Tamanhos disponíveis a partir de 127 GiB
- **Excluir com VM**: Opção que determina se o disco será automaticamente excluído quando a VM for deletada

### Discos de dados
- Adicione discos conforme necessidade de armazenamento
- Configure políticas de cache baseadas no uso
- **Excluir com VM**: Importante considerar esta opção para:
  - **Habilitar** quando o disco for temporário ou específico para aquela VM
  - **Desabilitar** quando o disco contiver dados que devem persistir após a exclusão da VM
  - Padrão recomendado para produção: Desabilitar para discos de dados importantes
 
  ### Observações importantes:
1. Discos marcados como "Excluir com VM" são permanentemente removidos quando a VM é deletada
2. Para dados críticos, sempre desmarque esta opção e implemente um backup separado
3. Discos temporários são sempre excluídos com a VM, independente desta configuração

## 8. Criando a VM

1. Revise todas as configurações
2. Clique em **Revisar + criar**
3. Após validação, clique em **Criar**
4. Acompanhe o processo de implantação

## Soluções pré-configuradas

Azure oferece stacks completos pré-configurados:
- **LAMP stack** (Linux, Apache, MySQL, PHP)
- **WordPress escalável**
- **VM Starter Kit** para início rápido

## Dicas de Dimensionamento

- Para desenvolvimento/teste: Série B (burstável)
- Para bancos de dados: Série E ou D (alto RAM/CPU)
- Para processamento batch: Série F
- Sempre considere alta disponibilidade para produção

## Monitoramento e Ajuste

Após criação:
1. Monitore desempenho no portal Azure
2. Ajuste tamanho conforme necessidade
3. Configure alertas para uso de recursos
