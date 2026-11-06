# <img width="30" height="30" alt="icone" src="https://github.com/user-attachments/assets/e299755d-1fe5-47c3-83e5-92a05cde71a8" /> AUT_1707 — Automação de Impressão em Lote (WinThor 1707) 

Sistema de automação inteligente desenvolvido para capturar códigos de produtos a partir de notas do **Google Keep** (via extensão de navegador), sincronizá-los com um servidor local e realizar a impressão automática em lote na **Rotina 1707 do ERP WinThor** (Ambiente Remoto) utilizando **AutoHotkey v2.0** e **Python (pywebview + Flask)**.

> ⚠️ **Aviso Importante:** A automação assume o controle do mouse e teclado durante o ciclo de impressão. Deixe o computador livre enquanto o robô estiver em execução para evitar falhas.

---

## 📥 Downloads e Instalação

1. **AutoHotkey v2.0:** Faça o download e instale a versão mais recente em [autohotkey.com](https://www.autohotkey.com/).
2. **Pacote da Automação:** Baixe o arquivo `Instalar_AUT_1707` na seção de **Releases** mais recente do repositório e extraia na pasta desejada.

---

## Principais Novidades e Funcionalidades

* **Modalidades Duplas de Inventário:** Separação total de filas, contagens diárias e indicadores para **Inventário Geral** e **Inventário Cíclico**.
* **Gravação Direta em Disco (File System Access API + IndexedDB):** Exportação direta do arquivo `codigos.csv` para a pasta `AUT 1707` sem acionar a janela de downloads do navegador ou requerer arrastar arquivos manualmente.
* **Reconexão de Pasta em 1 Clique:** Persistência da pasta vinculada no IndexedDB local com botão inteligente de reconexão de acesso (`Reconectar Pasta`) no cabeçalho web.
* **Processamento por Lotes Customizáveis:** Definição da quantidade de produtos por lote (ex: 20 por vez) com marcação automática de status de impressão no banco online.
* **Dashboard Analytics e Contagem:** Registro de contagem física diária, indicador visual de progresso (% contado vs. impresso) e gráfico comparativo dos últimos 7 dias.
* **Inicialização por Protocolo URI (`aut1707://start`):** Botão direto na aplicação web para abrir o executável `AUT_1707.exe` localmente.

---

## 📐 Arquitetura do Sistema

```
[ Painel Web Vercel / Neon DB ] ──────(Lote CSV)──────┐
│                                   │
(Google Keep Extension)                        ▼
│                    [ File System Access API ] ──> [ codigos.csv ]
▼                                (IndexedDB)              │
[ Servidor Local Python ] ───────────────────────────────────────────┤
│                                                         │
(Executa em Thread)                                         (Lido pelo AHK)
│                                                         │
[ AUT_1707.exe ] ──────(IPC Memória)──────> [ impressao_1707.ahk ] ──> [ WinThor 1707 ]

```

1. **Painel Web de Inventário (Vercel + Neon PostgreSQL):** Interface completa de gerenciamento da fila de impressão, controle de contagens físicas diárias, gráficos comparativos de 7 dias e gerador de lotes `codigos.csv`.
2. **Extensão Web (`extension_winthor`):** Extensão leve para Chrome/Edge que captura sequências numéricas de produtos do Google Keep e envia via HTTP POST para `http://localhost:5000/api/codigos` (sem Service Workers intermediários para evitar instabilidades).
3. **Servidor Local Python (`servidor_keep.py`):** Servidor Flask em segundo plano integrado ao aplicativo principal, responsável por receber os códigos do Keep e sincronizar localmente.
4. **Painel de Controle e Monitor (`AUT_1707.exe`):** Aplicativo gráfico (`pywebview`) para gerenciamento local, inicialização de processos, calibração de coordenadas $X, Y$ e exibição do painel de monitoramento em tempo real.
5. **Robô AutoHotkey (`impressao_1707.ahk`):** Script responsável pela automação de cliques, digitação, troca de impressora e tratamento de pop-ups no WinThor. Transmite o status para o painel via janela oculta em memória (IPC).

---

## Estrutura de Arquivos

```
AUT 1707/
├── AUT_1707.exe           # Aplicativo principal de controle e gerenciamento
├── _internal/             # Módulos compilados e dependências (PyInstaller --onedir)
├── impressao_1707.ahk     # Script robô do AutoHotkey v2
├── servidor_keep.py       # Servidor Flask local para recebimento do Keep
├── config.json            # Configurações de coordenadas, caminhos e impressora
├── codigos.csv            # Lista de códigos atualizada para processamento em lote
├── inventario.html        # Painel web principal de inventário e contagem
├── index.html             # Interface gráfica do painel de controle local
├── monitor.html           # Janela de status de impressão em tempo real
└── extension_winthor/     # Extensão para o navegador (manifest.json, content.js)

```
---

## 📺 Vídeo Tutorial (Passo a Passo)

Assista ao vídeo abaixo para ver a demonstração prática do funcionamento e o guia de configuração de todo o ecossistema:

https://github.com/user-attachments/assets/e0f92657-8802-41ba-a04e-c22647c0be6b

---

## 🖱 Configuração de pontos

Assista ao vídeo abaixo para ver como configurar a localização dos pontos de cliques do mouse na automação

https://github.com/user-attachments/assets/fc80860b-efd2-4e37-90d8-339cef59c470

---

## Exemplo de digitalização pro keep

Assista ao vídeo para ver um exemplo de como se pode digitalizar e enviar para o google keep

https://github.com/user-attachments/assets/0f0cfbe4-fb7c-4957-9b37-68f85356d64c

---

---

## Downloads e Instalação

1. **AutoHotkey v2.0:** Faça o download e instale a versão mais recente em [autohotkey.com](https://www.autohotkey.com/).
2. **Pacote da Automação:** Baixe o arquivo `automacao-impressao.zip` na seção de **Releases** mais recente do repositório e extraia na pasta desejada (de preferência nomeada como `AUT 1707`).

---

## Vídeo Tutorial (Passo a Passo)

Assista ao vídeo abaixo para ver a demonstração prática do funcionamento e o guia de configuração de todo o ecossistema:

https://github.com/user-attachments/assets/e0f92657-8802-41ba-a04e-c22647c0be6b

---

## Configuração de pontos

Assista ao vídeo abaixo para ver como configurar a localização dos pontos de cliques do mouse na automação:

https://github.com/user-attachments/assets/fc80860b-efd2-4e37-90d8-339cef59c470

---

## Exemplo de digitalização pro keep

Assista ao vídeo para ver um exemplo de como se pode digitalizar e enviar para o Google Keep:

https://github.com/user-attachments/assets/0f0cfbe4-fb7c-4957-9b37-68f85356d64c

---

## Como Utilizar (Passo a Passo)

### 1. Configuração Inicial da Pasta no Painel Web

1. Acesse a página do **Inventário** no painel web.
2. No cabeçalho, clique no botão **Configurar Pasta AUT 1707**.
3. Selecione a pasta onde o executável `AUT_1707.exe` está instalado.
4. *Observação:* Se recarregar a página ou fechar o navegador, o botão passará a exibir **Reconectar Pasta: AUT 1707**. Basta dar **1 clique** no botão para reautorizar a gravação direta.

### 2. Exportando Lotes para Impressão

1. Selecione a modalidade no topo da página (**Inventário Geral** ou **Inventário Cíclico**).
2. Adicione os códigos na **Entrada de Produtos** ou receba a fila sincronizada do banco de dados.
3. Defina a **Qtd. por Lote** (padrão: `20`).
4. Clique em **Exportar Lote CSV (Direto)**. O arquivo `codigos.csv` será gerado/sobrescrito diretamente na pasta local da automação e os itens serão marcados como impressos na nuvem.

### 3. Executando a Impressão no WinThor

1. Abra a **Rotina 1707** no ERP WinThor (preferencialmente maximizada no monitor calibrado).
2. Abra o aplicativo local clicando em **Abrir AUT 1707** no painel web (via protocolo `aut1707://start`) ou executando o **`AUT_1707.exe`**.
3. No aplicativo local, clique em **Abrir Script AHK** (ou pressione **`F2`** se o script já estiver ativo).
4. Selecione a modalidade de impressão:
   - **Impressão Direta:** Envia direto para a impressora padrão configurada na rotina (método mais rápido).
   - **Universal Printer:** Utiliza o fluxo com o software da impressora universal (método mais lento).
5. O robô assumirá o controle do teclado/mouse e processará cada código sequencialmente.

### 4. Sincronização via Google Keep (Método Alternativo)

1. Acesse o [Google Keep](https://keep.google.com/) no navegador com a extensão ativada.
2. Abra ou crie uma nota com a lista de códigos dos produtos.
   - *Dica:* Cada código deve ficar no início de uma linha. Exemplo de digitalização pela câmera do smartphone: copie o texto digitalizado e cole diretamente na nota do Keep.
3. O indicador **WinThor Sync: Ativo** surgirá no canto inferior da página, sincronizando os códigos diretamente com o arquivo `codigos.csv`.

---

## Relatórios Automáticos de Faltas/Impressão e Analytics

* **Fila x Contagem Física:** Permite registrar a quantidade contada no dia para conferência em tempo real da aderência do inventário (% de contados em relação aos impressos).
* **Gráfico de 7 Dias:** Histórico visual comparativo entre total de itens impressos e contados diariamente.
* **Relatórios Automáticos em CSV:** Toda impressão efetuada é registrada em um histórico local em `Relatorios_ANO/Relatorio_MES_ANO.csv` (Exemplo: `Relatorios_2026/Relatorio_11_2026.csv`) contendo **`CODIGO;DATA;HORARIO`**, pronto para abertura no Microsoft Excel ou Google Planilhas.

---

## Teclas de Atalho (Hotkeys)

| Tecla | Função |
| --- | --- |
| **`F1`** | **Pausar / Retomar** a automação em tempo real. |
| **`F2`** | **Iniciar** o processamento em lote dos códigos sincronizados. |
| **`F3`** | **Fechar / Encerrar** o script do AutoHotkey. |
| **`F4`** | **Importar Códigos do Clipboard:** Converte qualquer texto copiado com números em `codigos.csv`. |

---

## Calibração de Coordenadas (Mudança de Monitor/Resolução)

Se alterar a resolução do monitor ou mover a janela do WinThor:

1. No **`AUT_1707.exe`**, clique em **Configurar Painel**.
2. Clique no botão **Capturar** ao lado do campo que deseja recalibrar (a janela será minimizada).
3. Posicione o cursor do mouse sobre o campo/botão desejado na tela do WinThor e **clique com o Botão Direito**.
4. As coordenadas $X, Y$ serão atualizadas automaticamente.
5. Clique em **Salvar Configurações no Projeto**.

---

## Solução de Problemas Rápidos

* **Permissão negada ao exportar lote:** Clique no botão de aviso no cabeçalho (**Reconectar Pasta**) para renovar a autorização de gravação direta do navegador no disco local.
* **Navegador abrindo janela de Download em vez de salvar na pasta:** Certifique-se de estar utilizando o Google Chrome ou Microsoft Edge (navegadores com suporte à File System Access API).
* **Extensão indicando "Servidor Python desligado!":** Abra o `AUT_1707.exe` e confirme se clicou em **Iniciar Tudo**. Se necessário, clique em **Encerrar Tudo** e em seguida em **Iniciar Tudo**.
* **Extensão com mensagem "Extensão recarregada! Pressione F5":** Pressione a tecla `F5` na aba do Google Keep para atualizar a conexão do script na página.
* **Cliques fora do alvo no WinThor:** Verifique se a janela da Rotina 1707 está maximizada na mesma resolução de tela onde a calibração foi efetuada.
* **Processo AHK preso:** O botão **Encerrar Tudo** no aplicativo fecha especificamente o script `impressao_1707.ahk` sem afetar outros scripts AHK em execução no computador.

---

## Projeções de Desenvolvimento

* **Execução em Segundo Plano Ativa:** Pesquisa de soluções para interação via envio de mensagens diretas de controle (`ControlClick` / `ControlSend`) nas janelas do ambiente remoto do WinThor, permitindo que o operador continue utilizando o computador durante a impressão.
* **Tratamento Avançado de Exceções:** Identificação e desvio automático de bloqueios cadastrais ou de estoque na rotina 1707 sem interromper a fila de impressão.

---

## Suporte e Contato

Em caso de dúvidas, sugestões ou problemas na operação:

* **E-mail Corporativo:** gabriel.duarte@dellys.com.br
* **Microsoft Teams:** D8059GD@dellys.com.br / gabriel.duarte@dellys.com.br
* **E-mail Pessoal:** gabrieldgad2007@gmail.com
