# Olha o Achado! — Landing Page

Landing page de captação de leads para grupo de WhatsApp de afiliado de marketplace (Shopee + Mercado Livre), com foco em público feminino.

## Objetivo do projeto

Capturar leads via Meta Ads (CPL alvo: R$ 0,50–1,00) e levá-los para o grupo do WhatsApp **Olha o Achado!**, onde recebem ofertas curadas o dia inteiro via bot.

**Meta financeira:** 3 grupos cheios (~3.072 membros) gerando ~R$ 200/dia em comissões.

## Estrutura

```
lp-achadinhos/
├── index.html      # LP completa (HTML + CSS + JS inline)
├── ads-plano.md    # Plano de anúncios Meta Ads (estratégia, copy, criativos)
├── CLAUDE.md       # Este arquivo (contexto do projeto)
├── .mcp.json       # Config MCP servers (NÃO commitar — contém chaves)
└── .gitignore      # Ignora .mcp.json, .env, etc.
```

## Stack

- **HTML/CSS/JS puro** em arquivo único (`index.html`)
- Sem frameworks, sem build step, sem dependências
- Fontes via Google Fonts (Inter + Fraunces)
- Pixel da Meta integrado (substituir `SEU_PIXEL_ID` antes de subir)
- Hospedagem alvo: Netlify Drop ou Vercel (grátis)

## Decisões de design

- **Mobile-first** — 95%+ do tráfego virá de Reels/Feed Insta
- **Paleta:** creme + coral/terracotta + dourado suave (warm, feminino sem ser cafona)
- **Tipografia:** Fraunces (serif itálico nos destaques) + Inter (sans pro corpo)
- **Estilo "Claude design":** clean, cantos arredondados, sombras suaves, microanimações com propósito
- **Single-file** intencional — facilita deploy em qualquer host estático sem build

## Elementos de conversão na LP

1. Barra de urgência fixa no topo (countdown 24h regressivo)
2. Badge ao vivo "12.847 mulheres já entraram" (cresce automaticamente)
3. Barra de vagas com medidor visual (diminui sozinha)
4. Preview do grupo com mensagens animadas (bate a objeção "o que vou receber?")
5. Bullets de benefício com ícones
6. Comparativo "Sem o grupo vs Com o grupo"
7. Depoimento + 3 contadores animados
8. FAQ com accordion (5 perguntas — quebra objeções)
9. CTA final com urgência + selos de confiança
10. Toast flutuante "Maria de SP entrou agora" (rotaciona nomes/cidades)
11. Barra CTA fixa no mobile que aparece após 600px de scroll

## Antes de subir pra produção

- [ ] Trocar `SEU_PIXEL_ID` no `<script>` Meta Pixel (linha ~17 do `index.html`)
- [ ] Trocar `WHATSAPP_GROUP_LINK` na constante JS (final do `index.html`)
- [ ] Verificar domínio no Meta Events Manager (crítico pós-iOS 14)
- [ ] Configurar evento "Lead" como prioridade #1 no Aggregated Event Measurement
- [ ] Criar um favicon (`/favicon.ico`)
- [ ] Atualizar nomes/cidades dos toasts se quiser personalizar
- [ ] Trocar números falsos do contador inicial (ex: 12.847) por números reais quando subir

## Convenções de código

- **Nada de framework, nada de build** — single HTML autossuficiente
- **CSS inline no `<head>`** — evita request extra
- **JS inline no fim do `<body>`** — sem dependências externas
- **Mobile-first responsivo** — usar `clamp()` pra tipografia fluida
- **Sem comentários óbvios no código** — só comentar o "porquê" não-trivial
- **Acessibilidade básica:** `prefers-reduced-motion`, `safe-area-inset`, `min-width 320px`

## Bot de afiliado (fora deste repositório)

Este projeto é só a LP. O bot que envia 1.500 ofertas/dia nos grupos roda separado, integrando com APIs de afiliados da Shopee e Mercado Livre.

## Configurações do Claude Code

- **MCPs disponíveis** (via `.mcp.json`): GitHub, BrowserMCP, SSH, Postgres, Stripe, ElevenLabs, Canva, NanoBanana (Gemini image)
- **Use `nanobanana`** quando precisar gerar imagens (logo do grupo, criativos de anúncios)
- **Use `canva`** pra editar designs já existentes
- **Use `elevenlabs`** pra gerar voz off pros Reels UGC
- **Use `browsermcp`** se precisar testar a LP em browser real
- **NÃO commitar** o `.mcp.json` — está no `.gitignore`

## Próximos passos sugeridos

- Gerar logo do grupo "Olha o Achado!" (ver opções de prompt na conversa)
- Criar 3 scripts de Reels UGC (formato cena por cena)
- Configurar pixel Meta + verificar domínio
- Hospedar LP no Netlify e testar em mobile real
- Subir 1ª campanha de R$ 50/dia conforme plano em `ads-plano.md`
