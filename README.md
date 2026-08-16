# Carreira Visual

Plataforma de cursos, mentorias e conteúdos de fotografia, filmmaking e carreira audiovisual de **Marcos Prado**.

**Produção:** [carreiravisual.com.br](https://carreiravisual.com.br)

HTML, CSS e JavaScript puros. Sem framework, sem build, sem dependência. O que está no repositório é exatamente o que vai para o ar.

---

## Estrutura

```
index.html ......................... a plataforma (home, busca, catálogo, tudo)
images/ ............................ capas dos produtos e fotos autorais (.webp)
o-que-fica/ ........................ landing page do curso
lap/
corre-y-cria/
domine-sua-fuji/
quadros-lucrativos/
masterclass-documentario-esportivo/
mentoria-direcao/
vintagefilm/
presets-fuji/
.htaccess .......................... HTTPS, cache e compressão (Apache / cPanel)
netlify.toml ....................... cache e cabeçalhos (Netlify / Cloudflare Pages)
_redirects ......................... página de erro (Netlify / Cloudflare Pages)
```

**Pasta = endereço.** A pasta `lap/` com um `index.html` dentro vira `carreiravisual.com.br/lap`.
Os arquivos de configuração das duas hospedagens convivem sem conflito: cada serviço lê só o dele.

---

## Onde editar

Tudo o que muda no dia a dia está no topo da tag `<script>` do `index.html`, em três objetos:

| Objeto     | O que controla                                                              |
|------------|-----------------------------------------------------------------------------|
| `CONFIG`   | redes sociais, e-mail, WhatsApp, links dos cursos, IDs do YouTube, tempo do hero |
| `PRODUCTS` | os nove produtos: capa, categoria, descrição, tópicos, tags                  |
| `VIDEOS`   | vídeos do YouTube exibidos na plataforma                                     |
| `HERO`     | quais capas entram no rodízio do topo e em que ordem                         |
| `PHOTOS`   | galeria autoral da home e da página de portfolio                             |

Nada disso exige mexer em CSS ou em layout.

---

## Adicionar um curso novo

1. Coloque a capa **vertical (2:3)** e a **horizontal (16:9)** em `images/`, em `.webp`
2. Copie um bloco do array `PRODUCTS` e troque os campos
   (`cover` = vertical, `wide` = horizontal, `rows` = em quais fileiras aparece)
3. Crie a pasta do curso com o `index.html` da landing page dentro
4. Aponte `CONFIG.links` para essa pasta
5. Se for destaque, adicione no array `HERO`

---

## Padrão de imagem

- Formato **WebP**, qualidade **92**, na resolução original — sem redimensionar
- Vertical **2:3** · Horizontal **16:9**
- Artes com meio-tom, grão ou textura pesam mais. Não baixe a qualidade nelas:
  é justamente onde o artefato de compressão aparece

---

## Detalhes de implementação

- **Rotas** por hash (`#/cursos`, `#/explorar`), renderizadas em JavaScript a partir dos dados
- **Hero** troca as capas sozinho; o intervalo vem de `CONFIG.heroInterval`
- **Capa responsiva**: `<picture>` entrega a vertical até 900px e a horizontal acima disso,
  e o navegador baixa só a que vai usar
- **Card estilo Netflix TV**: no hover a miniatura vertical cresce e vira a capa horizontal.
  A horizontal só é baixada no primeiro hover daquele card
- **Sem localStorage** e sem cookies

---

## Publicar

**Automático (recomendado):** conecte este repositório na Netlify, Vercel ou Cloudflare Pages.
Sem comando de build, diretório de publicação `.` — cada `git push` republica o site.

**Manual (cPanel):** envie o conteúdo da pasta para `public_html` e rode o AutoSSL.

---

© Marcos Prado — todos os direitos reservados sobre as imagens e o conteúdo.
