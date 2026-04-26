# TODO — Olha o Achado!

Itens pendentes pra evoluir o setup depois do MVP rodando.

---

## 🔴 Crítico — fazer assim que tiver tração

### Comprar domínio próprio + verificar na Meta

**Por quê:** sem domínio verificado, o Pixel da Meta perde **30-50% das conversões pós-iOS 14**. Isso significa que o painel mostra menos leads do que realmente está chegando, dificulta otimizar e infla o CPL aparente.

**Bloqueio descoberto em 26/04/2026:**
A Meta NÃO permite verificar subdomínios de plataformas (`olhaoachado.netlify.app` é subdomínio de `netlify.app`, que está na "public suffix list" da Meta). Mensagem do form de adicionar domínio:
> "Você só pode verificar o domínio raiz (exemplo.com), e não um subdomínio (loja.exemplo.com)"

**Ação:**
1. Comprar `olhaoachado.com.br` no [Registro.br](https://registro.br) (~R$ 40/ano, paga em PIX)
   - Alternativa: `olhaoachado.com` no Cloudflare/Namecheap (~$10/ano, propaga mais rápido)
2. Apontar DNS pro Netlify:
   - No Netlify: Project `olhaoachado` → Domain settings → Add custom domain `olhaoachado.com.br`
   - No Registro.br: configurar 2 registros DNS:
     - `A` → `75.2.60.5` (IP do Netlify load balancer)
     - `CNAME www` → `olhaoachado.netlify.app`
   - Aguardar propagação DNS (10min a 24h)
3. Voltar em Business Manager → Desafio Meta → Domínios → Adicionar `olhaoachado.com.br`
4. Escolher método "Meta Tag" → copiar a tag `<meta name="facebook-domain-verification" content="...">`
5. Adicionar essa tag no `<head>` do `index.html` (logo após `<meta name="description">`)
6. `git add index.html && git commit -m "add fb domain verification" && git push` + redeploy Netlify
7. Voltar na Meta → "Verificar" → aguarda 24h se não verificar na hora

---

## 🟡 Importante — fazer no mês 1

### Migrar Pixel pro Business "Desafio Meta"

**Estado atual:**
- Pixel `25245409135083896` (nome "API oficial tutorial") está dentro do Business `recuperarfoto.ia` (outro projeto pessoal)
- Estamos rodando anúncios pelo Business `Desafio Meta`
- Funciona, mas mistura projetos no Events Manager

**Ação:**
1. No Business Manager → Desafio Meta → Conjuntos de dados → Criar Pixel "Olha o Achado"
2. Pegar novo Pixel ID (16 dígitos)
3. Trocar `fbq('init', '25245409135083896')` no `index.html` pelo novo ID
4. Redeploy
5. (Opcional) Renomear pixel antigo no `recuperarfoto.ia` ou deletar se sobrou de tutorial

### Resolver restrição do Business "Olha o Achado"

**Estado:** o Business novo "Olha o Achado" (ID `26580909578261025`) foi criado mas caiu em restrição automática:
> "Portfólio empresarial com restrições para anunciar — Não é possível usar a empresa Olha o Achado para veicular anúncios, gerenciar contas de anúncios ou usar fontes de dados como pixels"

**Caminho:**
1. Acessar https://business.facebook.com/accountquality/advertising_access/?id=26580909578261025
2. Submeter apelação (geralmente pede ID + selfie)
3. Aguardar 24-72h
4. Se aprovado, migrar tudo da `Desafio Meta` pra esse Business (mais limpo)

---

## 🟢 Bom ter — fazer no mês 2-3

### Open API Shopee
**Estado atual:** API bloqueada (precisa de histórico de vendas pra liberar)
**Ação:** após gerar primeiras vendas (~30 dias de campanha), pedir acesso via "Entre em contato" no painel `affiliate.shopee.com.br/open_api`

### Mudar conta Shopee Afiliados de "Individual" pra "Empresa"
**Por quê:** tipo "Empresa" tem prioridade na fila do Open API + comissões um pouco melhores
**Ação:** entrar com MEI (R$ 70/mês de imposto) ou CNPJ existente

### Vincular Instagram à Página
**Estado atual:** Página FB "Olha o Achado" criada, mas sem Instagram conectado
**Ação:** criar conta `@olhaoachado` no Insta (ou usar `@eduardosouza.dev` mesmo) → conectar na Página → vai permitir anúncios em Reels/Stories Insta também

### Configurar Meta Pixel CAPI (Conversions API)
**Por quê:** roda do server-side, não depende de cookies do navegador → mais 10-20% de attribution
**Ação:** integrar via Netlify Functions ou Webhook do bot WhatsApp

---

## ⚪ Nice to have

- Comprar `.com.br` + `.com` (defensivo, R$ 90 total)
- Adicionar página de Política de Privacidade (`/privacidade`) — exigência LGPD
- Adicionar Google Analytics 4 + UTMs nos anúncios
- A/B testar 3 variações de hero copy
- Configurar pixel de conversão também no link do WhatsApp (event `Contact` ou `CompleteRegistration` no momento que o usuário entra no grupo — via webhook)
- Migrar de GitHub Pages (pode desligar a duplicata em https://deveduardosouza.github.io/lp-achadinhos/)

---

## Notas técnicas relevantes

**IDs e referências:**
- Pixel ID atual: `25245409135083896` (em `recuperarfoto.ia`)
- Página FB ID: `61562843709133` (em perfil pessoal, ainda não vinculada a Business)
- Business `Desafio Meta` ID: `1030026333524534`
- Conta de anúncios usada: `1257753845488824`
- ID Afiliado Shopee: `18390690958`
- Repo GitHub: https://github.com/DevEduardoSouza/lp-achadinhos
- Site Netlify ID: `869695d8-9a29-4efb-a530-6195e1c75118`
- WhatsApp invite: `https://chat.whatsapp.com/JGfmcIPC73gLQBgFcfyojf?mode=gi_t`
