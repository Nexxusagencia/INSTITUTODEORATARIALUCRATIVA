# LP — Instituto Oratória Lucrativa

Landing page do **treinamento online de comunicação** do Instituto Oratória Lucrativa.
Página estática, um arquivo só, sem build e sem dependências.

---

## Estrutura

```
index.html                      página completa (HTML + CSS + JS inline)
img/
  hero-escritorio.jpg           foto do hero
  palco-instituto.jpg           foto da seção "Por que começar agora"
  treinamento-online.jpg        foto da seção de oferta
  logo-instituto.png            símbolo da marca (versão fundo escuro, com transparência)
  og-instituto.jpg              imagem de compartilhamento — 1200×630
netlify.toml                    cabeçalhos de cache e segurança
```

Fontes vêm do Google Fonts (Newsreader + Archivo). Todo o resto é local.

---

## Antes de publicar — checklist

- [ ] **Trocar `SEU-DOMINIO.com.br`** nas tags `canonical`, `og:url` e `og:image` do `index.html`
- [ ] **Ativar o GA4**: descomentar o bloco no `<head>` e trocar `G-XXXXXXXXXX`
- [ ] **Ativar o Meta Pixel**: descomentar o bloco e trocar `SEU_PIXEL_ID`
- [ ] **Conferir o número do WhatsApp** — hoje está `5515 3198-0182`, em 6 links.
      São 8 dígitos começando em 3 (formato de telefone fixo). Se o WhatsApp for
      celular, falta o 9º dígito e **todos os botões param de funcionar**. Teste
      abrindo a página de um celular antes de subir.
- [ ] Publicar em **domínio próprio** (não em subdomínio de plataforma)

---

## Animações

Entrada escalonada no hero (CSS puro) e revelação das seções ao rolar
(IntersectionObserver, no fim do `index.html`). Botões têm elevação e brilho
ao passar o mouse, e afundam ao clicar.

Salvaguardas ativas:

- **Sem JavaScript** a página aparece inteira — nada fica preso em `opacity: 0`
- O script marca e revela no mesmo quadro, então não existe piscada de conteúdo
- Rede de segurança: se o observador falhar, tudo aparece 1,2s após o `load`

**Decisão do cliente:** as animações rodam em todas as máquinas, inclusive nas que
pedem movimento reduzido no sistema operacional. O bloco
`@media (prefers-reduced-motion: reduce)` está comentado no `<style>`, junto com a
verificação de `matchMedia` no `<script>` — basta descomentar os dois para voltar a
respeitar essa preferência.

Para remover o movimento por completo, apague as regras de animação do `<style>`
e o `<script>` do fim do arquivo.

---

## Rastreamento de CTA

Já existe no fim do `index.html` um script que dispara um evento a cada clique em
botão de WhatsApp, identificando a seção de origem pelo rótulo (`.eyebrow`) da seção.

- GA4: evento `clique_whatsapp`, com os parâmetros `secao` e `texto`
- Meta: evento padrão `Contact`, com `content_name` = seção

Ele só começa a enviar dados depois que o GA4 e/ou o Pixel forem ativados no `<head>`.
Cada botão também abre o WhatsApp com uma mensagem própria, escrita na voz do lead,
o que permite identificar a origem do contato direto na conversa.

---

## Rodar localmente

Abrir o `index.html` no navegador já funciona. Para servir por HTTP:

```bash
python -m http.server 8080
# http://localhost:8080
```

---

## Publicar

**Netlify** — arraste a pasta em app.netlify.com/drop, ou conecte este repositório
(sem comando de build; diretório de publicação: a raiz).

**GitHub Pages** — Settings → Pages → Source: `main` / raiz.

**Vercel** — importar o repositório, framework "Other", sem build.

---

## Conteúdo da página

Sete seções, na ordem:

1. Hero — headline e primeiro CTA
2. Por que desenvolver sua comunicação
3. Comunicação é mais do que falar bem — expressão / persuasão / liderança
4. Como o Instituto pode me ajudar — situações reais de aplicação
5. Para quem é esse treinamento — quatro perfis
6. Por que começar agora
7. Oferta e CTA final

A página **não exibe preço**: os seis CTAs levam ao WhatsApp, e o valor é
apresentado no atendimento.

---

## O que ainda falta (recomendações)

- **Depoimentos de alunos** — maior lacuna de conversão da página hoje
- **Bloco de autoridade do professor** com trajetória prática e números
- **FAQ** cobrindo acesso, prazo, suporte e reembolso
- **Garantia** declarada
- **Formulário de captura** como alternativa ao WhatsApp, para construir lista
