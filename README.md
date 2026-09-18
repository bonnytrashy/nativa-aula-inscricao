# Nativa — Aula ao vivo e gratuita (Landing de inscrição)

Landing page de captação para a aula **Tendências de Salão 2026** com Denize, fundadora da Nativa.
Página única, sem rolagem (hero em `100vh`), captura a inscrição em um modal de 2 etapas e
redireciona a pessoa para o grupo de WhatsApp.

## Stack
HTML/CSS/JS puro. Sem build, sem framework. Abre localmente com duplo clique e publica em qualquer host estático.

## Estrutura
```
index.html        # página + modal + lógica de envio
assets/
  denize.png      # foto da Denize (direita / fundo no mobile)
  logo.png        # logo "ntv | linha profissional" (rodapé)
  produtos.png    # linha de produtos (não usada no layout atual, disponível)
vercel.json       # config de deploy estático (cache dos assets)
```

## Configuração
No topo do `<script>` em `index.html`, ajuste o objeto `CONFIG`:

| Campo | O que é |
|---|---|
| `WHATSAPP_GROUP_URL` | Grupo para onde a pessoa é redirecionada após o cadastro |
| `WEBHOOK_URL` | Endpoint que recebe o lead via POST (JSON). Vazio = desligado |
| `META_PIXEL_ID` | Se preenchido, dispara o evento `Lead` do Meta Pixel |
| `WEBHOOK_TIMEOUT_MS` | Timeout curto do POST — o redirect nunca é travado |

Os dados enviados incluem: nome, WhatsApp, as 5 respostas, `timestamp` e os parâmetros de
UTM da URL (`utm_source`, `utm_medium`, `utm_campaign`, `utm_content`, `utm_term`).
Uma cópia de backup fica em `localStorage` (`nativa_lead`).

> Para ligar RD Station / GoHighLevel / Zapier, há um bloco comentado marcado no `submit`.

## Deploy
- **Vercel:** importe o repositório (sem build; framework "Other"). O `vercel.json` cuida do resto.
- **Qualquer host estático:** suba `index.html` + `/assets`.

## Trocar imagens
Basta substituir os arquivos em `/assets` mantendo os nomes. Os caminhos estão comentados no HTML.
