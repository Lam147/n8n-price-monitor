# 🛒 n8n - Monitor de Preços e Alerta de Telegram

Este repositório contém um workflow (fluxo de trabalho) n8n para monitorar o preço de um produto em um site (usando Web Scraping) e enviar uma notificação via Telegram caso o preço caia abaixo de um valor predefinido.

## 🛠️ Detalhes do Workflow

O fluxo de trabalho opera da seguinte forma:

1.  **Gatilho (Cron):** Inicia a automação em intervalos regulares (configurado para rodar diariamente).
2.  **HTTP Request:** Acessa a URL da página do produto.
3.  **Cheerio:** Faz o web scraping para extrair o preço atual do produto na página HTML.
4.  **IF:** Verifica se o preço extraído é menor do que o preço alvo (R$ 1.500,00 no exemplo).
5.  **Telegram:** Se a condição for verdadeira, envia um alerta de queda de preço.

## 🚀 Como Colar e Usar na sua Instância n8n

### Passo 1: Importar o Workflow

1.  Copie o conteúdo do arquivo `price-monitor-workflow.json` deste repositório.
2.  Acesse sua instância do n8n (Cloud ou Local).
3.  Crie um novo workflow e clique em **"Import from JSON"** (Importar de JSON).
4.  Cole o código copiado e importe.

### Passo 2: Configurar Credenciais e Alvo

Após a importação, você precisa fazer as seguintes modificações nos nodes:

1.  **Node `HTTP Request`:**
    * Substitua a URL de exemplo (`https://www.exemplo-loja.com/produto-exemplo`) pela URL do produto real que você deseja monitorar.

2.  **Node `Cheerio`:**
    * Ajuste o `cssSelector` (`.price-area .final-price`) para o **seletor CSS correto** onde o preço é exibido na página do seu produto.

3.  **Node `Send Telegram Alert`:**
    * **Crie as credenciais do Telegram:** Adicione um **Bot Token** e configure o **Chat ID** (o ID do chat ou grupo para onde a mensagem será enviada).
    * No node, selecione a credencial que você acabou de criar.

4.  **Node `IF Price Drop`:**
    * Você pode alterar o valor de comparação (`1500`) para o preço máximo que você está disposto a pagar.

### Passo 3: Ativar

1.  Após configurar todos os nodes e credenciais, clique no botão para **"Ativar"** (**Activate** / **Active**).
2.  O workflow rodará automaticamente no horário configurado pelo node **Cron**.
