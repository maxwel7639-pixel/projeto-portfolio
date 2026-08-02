# Portfólio MX Digital

Página de portfólio da MX Digital — 13 sites entregues para negócios de estética,
terapias e psicologia no Rio Grande do Sul.

Site estático, sem build. Basta servir a pasta.

```
index.html              página inteira (HTML + CSS + JS inline)
assets/logo-mx.png      logo da marca (header + favicon)
assets/proj-*.webp      prints desktop dos 13 sites (usados acima de 720px)
assets/mob-*.webp       prints mobile dos 13 sites (usados até 720px)
```

A paleta e o fundo do hero são os mesmos do mxdigital.ia.br — roxo
`#8B2FD4`/`#A855F7` e magenta `#d81b93`/`#ff3db0`. Se o site principal mudar de
identidade, é aqui que precisa acompanhar.

## Rodar local

```bash
python3 -m http.server 8000
# http://localhost:8000
```

## Deploy (Vercel)

Add New → Project → importar o repositório → Framework **Other**, Build e Output
vazios, Root Directory na raiz. O `index.html` está na raiz, então não precisa de
configuração extra.

## Editar os projetos

Toda a lista vive no array `PROJECTS`, no `<script>` no fim do `index.html`.
Os contadores dos filtros e o "01 / 13" dos cards são calculados a partir dela —
não precisa mexer em mais nada ao adicionar ou remover um projeto.

```js
{id:'kauana', name:'Kauana Liesenfeld', cat:'estetica', badge:'Estética',
 desc:'...', url:'https://kauana-liesenfeld.vercel.app'}
```

`cat` precisa ser `estetica`, `terapias` ou `psicologia` (é o que os filtros usam).

## Os prints dos sites

Cada card é um frame com uma barra no topo que mostra o domínio real, o nicho e
a numeração. Dentro dela vai o print do site. São **dois prints por projeto**,
servidos por `<picture>` conforme a largura da tela:

```js
{id:'kauana', ...,
 src:   'assets/proj-kauana.webp',   // desktop, acima de 720px
 srcMob:'assets/mob-kauana.webp'}    // mobile, até 720px
```

O navegador baixa só o que vai usar, então nenhum aparelho carrega os dois.

Se um projeto **não** tiver `src`, o card cai automaticamente no modo mockup:
mesmo frame, mas com as iniciais do cliente em degradê no lugar do print. Serve
pra publicar um projeto novo antes de ter a captura pronta. O `srcMob` é
opcional — sem ele o print desktop é usado em qualquer largura.

### Trocar ou adicionar um print

- **Desktop** (`proj-{id}.webp`): captura do hero em ~2:1, 1600px de largura.
  A proporção é preservada, sem corte.
- **Mobile** (`mob-{id}.webp`): captura do site aberto no celular, ~700px de
  largura. Corte a barra de status do sistema (relógio/bateria) antes de salvar.
  No card ela preenche a largura toda e o excedente é cortado pelo rodapé.

Nos dois casos o que importa é o **topo** do print — logo, headline e botão
principal —, porque é o que sempre aparece.

Vale manter os arquivos leves: os 13 prints desktop dão ~356 KB e os 13 mobile
~596 KB, em webp. Os originais em PNG/JPEG davam 3,2 MB e 1,5 MB.

### Ordem dos cards

É a ordem do array `PROJECTS`, e vale para os dois lugares (carrossel e stack de
scroll) ao mesmo tempo. Para promover um cliente, basta mover a linha dele.

## Antes de publicar em domínio próprio

As meta tags Open Graph no `<head>` apontam para `https://mxdigital.ia.br`.
Se o portfólio for para outro endereço, atualizar `og:url`, `og:image`,
`twitter:image` e o `<link rel="canonical">`.
