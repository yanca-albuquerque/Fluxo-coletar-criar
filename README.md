# Automação de Coleta de E-mails com Power Automate e Graph API

### Visão Geral

Este projeto é um fluxo de nuvem construído no Microsoft Power Automate, projetado para monitorar uma caixa de e-mail compartilhada, coletar e processar e-mails, e registrar as informações em uma lista do SharePoint.

### Principais Funcionalidades

- **Busca em Múltiplas Pastas:** Monitora tanto a "Caixa de Entrada" quanto os "Itens Enviados" para ter uma visão completa das conversas.
- **Comunicação Direta com a API Graph:** Usa a ação HTTP para fazer chamadas diretas à API do Microsoft Graph, permitindo filtros avançados (`$filter`, `$select`, `$orderby`) e a extração de metadados complexos, como os `internetMessageHeaders`.
- **Paginação:** Lida com grandes volumes de e-mails através de um loop de paginação (`Fazer até`) que segue o `@odata.nextLink` da API.
- **Enriquecimento com IA:** Utiliza o AI Builder (GPT) para gerar resumos técnicos e extrair palavras-chave do corpo dos e-mails.

### Tecnologias Utilizadas

-   Microsoft Power Automate
-   Microsoft Graph API
-   SharePoint Online (Listas)
-   Expressões do Power Automate (WDL)
-   AI Builder (GPT)

### Como Funciona

1.  **Gatilho:** O fluxo é iniciado por um gatilho de recorrência diário.
2.  **Coleta de Dados:** Um loop `Aplicar a cada` itera sobre as pastas definidas ("Inbox", "SentItems"). Dentro dele, um loop `Fazer até` chama a API Graph repetidamente para buscar todas as "páginas" de e-mails do período calculado.
3.  **Agregação:** Todos os e-mails coletados são armazenados em uma única variável do tipo matriz (`todosEmails`).
4.  **Processamento da Conversa:** Para cada conversa única:
    * Filtra a matriz `todosEmails` para pegar todos os e-mails daquela conversa.
    * Executa as ações de enriquecimento (busca em tabela Excel, chamadas ao AI Builder, etc.).
    * Cria um único item na lista do SharePoint com os dados consolidados.

#### 💡 Dica: Caso de dúvidas ou sugestões, fique à vontade para abrir entrar em contato.
