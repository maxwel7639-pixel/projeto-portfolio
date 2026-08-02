# Portfólio MX Digital

Página de portfólio da MX Digital — 13 sites entregues para negócios de estética,
terapias e psicologia no Rio Grande do Sul.

Site estático, sem build. Basta servir a pasta.

```
index.html              página inteira (HTML + CSS + JS inline)
assets/logo-mx.png      logo da marca (header + favicon)
assets/proj-*.webp      prints dos 13 sites
```

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

Cada card é um frame de navegador com o domínio real na barra de endereço e o
print do site dentro. O print aparece nos dois lugares — carrossel e stack de
scroll — a partir do campo `src`:

```js
{id:'kauana', ..., src:'assets/proj-kauana.webp'}
```

Se um projeto **não** tiver `src`, o card cai automaticamente no modo mockup:
mesmo frame de navegador, mas com as iniciais do cliente em degradê no lugar do
print. Serve pra publicar um projeto novo antes de ter a captura pronta.

### Trocar ou adicionar um print

Prints são capturas do hero, ~2:1 (1600×760 fica ótimo), salvas em `.webp` como
`assets/proj-{id}.webp`. O nome não é mágico — o que vale é o `src` no
`PROJECTS` — mas seguir o padrão facilita.

A proporção é preservada no desktop (a imagem não é esticada nem cortada). No
celular os cards são bem mais altos que 2:1, então o print recebe um corte pelo
topo — 4:3 no card grande, 16:10 no card do carrossel. Por isso o que importa
mais é o **topo** do print: logo, headline e botão principal.

Vale manter os arquivos leves: os 13 prints juntos dão ~356 KB em webp. Os
mesmos em PNG davam 3,2 MB.

## Antes de publicar em domínio próprio

As meta tags Open Graph no `<head>` apontam para `https://mxdigital.ia.br`.
Se o portfólio for para outro endereço, atualizar `og:url`, `og:image`,
`twitter:image` e o `<link rel="canonical">`.
