# ONNE — Landing page

Página de conversão da **ONNE | Revenda Autorizada DJI** (São Carlos/SP).
Arquivo único, sem build: `index.html`.

---

## 1. Como ver a página

Dê dois cliques em `index.html` — abre no navegador.

Para simular o comportamento real (recomendado antes de publicar), rode um servidor local:

```powershell
cd "C:\Users\rolda\Documents\Codigos\J-Embare\ONNE"
python -m http.server 8080
# depois abra http://localhost:8080
```

---

## 2. Paleta (extraída das artes oficiais da ONNE)

Todos os valores dos posts do Instagram `@somos.onne` foram amostrados pixel a pixel:

| Token | Hex | Onde é usado |
|---|---|---|
| `--lime` | `#97C11F` | cor da marca (o "NN" verde), botões, formas diagonais |
| `--lime-700` | `#647E12` | texto verde sobre fundo claro (contraste) |
| `--bg` | `#F5F5F3` | fundo da página (as artes usam `#F0F0F0`) |
| `--ink` | `#2E2E2B` | títulos |
| `--charcoal` | `#4A4A4A` | corpo de texto (cor real das artes) |
| `--dark` | `#25280F` | seções escuras (Sobre e Contato) |

**Para trocar a paleta inteira:** altere só o bloco `:root` no topo do `<style>` em `index.html`.

A logo é feita em HTML (`O`**`NN`**`E`), reproduzindo o destaque verde do "NN" que aparece nas peças da marca. Não depende de arquivo de imagem, então nunca quebra.

---

## 3. O que substituir (placeholders)

> **Modo edição:** os avisos `[PLACEHOLDER]` ficam **escondidos** na página publicada — o visitante nunca lê "placeholder". Para vê-los, abra a página com `?dev` na URL:
> `index.html?dev` (ou `http://localhost:8080/index.html?dev`).
> Para localizar no código, busque por `PLACEHOLDER` no `index.html` (Ctrl+F).

### 3.1 Fotos — apenas sobrescreva o arquivo, mesmo nome e pasta

| Arquivo | Tamanho ideal | O que deve ser |
|---|---|---|
| `assets/foto-hero.jpg` | 1400 × 1050 | Drone em voo, fachada ou equipe |
| `assets/foto-sobre.jpg` | 1200 × 900 | Equipe / fachada da loja |
| `assets/og-cover.jpg` | 1200 × 630 | Imagem de compartilhamento (WhatsApp/Instagram) |
| `assets/fotos/produto-*.jpg` | 900 × 700 | Foto de cada equipamento |

Não precisa mudar nada no código — os nomes em `index.html` já são esses.

### 3.2 Outros

| O que | Onde |
|---|---|
| Selo oficial "Revenda Autorizada DJI" | seção "faixa de confiança" (`<!-- PLACEHOLDER -->`) |
| Preços / combos / parcelamento | cards em `#equipamentos` (hoje todos "Sob consulta") |
| Horário de funcionamento | seção `#contato` (não está cadastrado no Google) |
| E-mail comercial | rodapé |
| CNPJ | rodapé |
| Formas de pagamento | resposta do FAQ |
| Escopo da assistência técnica | resposta do FAQ |
| Depoimentos de clientes | bloco comentado na seção "Para quem a ONNE voa" |
| Google Analytics / Meta Pixel | comentário no `<head>` |

---

## 4. Contatos e links usados

| Item | Valor |
|---|---|
| WhatsApp | `5516997554669` — mudar em 3 lugares: constante `WA` no JS, `#fab` e o link do rodapé |
| Telefone | `(16) 99755-4669` |
| Instagram | https://www.instagram.com/somos.onne/ |
| Endereço | Av. João Orlando Ruggiero, 45 — Jardim Embaré, São Carlos/SP, 13563-840 |
| Mapa | embed por coordenadas `-21.9708273, -47.9314889` |
| Google Maps | https://maps.app.goo.gl/sL1PZAamrfw3h7j79 |

---

## 5. GitHub Pages — já publicado

| | |
|---|---|
| Repositório | https://github.com/roldan-eng-software/onne |
| **Site no ar** | **https://roldan-eng-software.github.io/onne/** |
| Branch publicada | `main` (raiz do repositório) |
| HTTPS | forçado (automático pelo GitHub) |

Configuração: **Settings → Pages → Source: Deploy from a branch → `main` / `/ (root)`**.
O `.nojekyll` já está incluído para o GitHub Pages não processar os arquivos com Jekyll.

### Como atualizar o site depois de uma alteração

```powershell
cd "C:\Users\rolda\Documents\Codigos\J-Embare\ONNE"
git add .
git commit -m "Descreva aqui o que mudou"
git push
```

O GitHub republica sozinho em ~1 minuto. Nada de build, nada de instalar dependência.

> **Atenção:** o `.gitignore` ignora a pasta `.opencode/` (configurações locais do editor). Ela não vai para o site — e não deve ir.

### Domínio próprio (opcional, mais à frente)
Se registrarem `somosonne.com.br`:
1. Crie um arquivo `CNAME` na raiz do repositório com o domínio dentro (só isso, uma linha).
2. No DNS, aponte para o GitHub Pages (registros `A` para os IPs do GitHub + `CNAME` de `www`).
3. Marque **Enforce HTTPS** em Settings → Pages.
4. Troque a `<link rel="canonical">` e as URLs de `og:image` / `twitter:image` / JSON-LD no `index.html` para o domínio novo — hoje elas apontam para a URL do GitHub Pages.

---

## 6. Como a conversão funciona

- **Toda ação leva ao WhatsApp.** Cada botão abre a conversa com uma mensagem já contextualizada (o visitante não precisa escrever nada).
- **Formulário → WhatsApp.** O formulário da seção Contato monta a mensagem com nome, segmento e necessidade e abre o WhatsApp. Não há backend, não há risco de e-mail cair em spam.
- **Botão flutuante** de WhatsApp em todas as telas.
- **Barra fixa no mobile** (Orçamento / Ligar) que aparece após o primeiro scroll.
- **CTA a cada 1–2 seções**, para capturar quem entra no meio da página.
- **Funciona sem JavaScript**: os links de WhatsApp já estão escritos no HTML e o FAQ usa `<details>` nativo.

---

## 7. Observações importantes

1. **Não há prova social real.** A ONNE tem perfil novo e **nenhuma avaliação no Google**. Os depoimentos estão comentados no código de propósito — não invente clientes. Peça avaliação no Google nas primeiras vendas: é o que mais converte em busca local.
2. **Confirme o WhatsApp.** O número `(16) 99755-4669` está publicado no Google. Certifique-se de que ele está ativo no WhatsApp Business antes de divulgar o site.
3. **Selo DJI.** O texto "Revenda autorizada DJI" é um fato verificado (está no nome do perfil oficial da empresa). Já o **logo** da DJI é marca registrada e tem regras de co-branding — use o material oficial que a DJI fornece a revendas autorizadas.
4. **SEO local.** Já existe `JSON-LD` do tipo `Store` com endereço, telefone e geolocalização. Ao publicar, vincule a URL do site ao perfil do Google Meu Negócio — hoje o perfil não tem site associado, e isso ajuda muito no ranking local.
