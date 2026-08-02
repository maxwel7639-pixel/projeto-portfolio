# Portfólio MX Digital

Página de portfólio da MX Digital — 13 sites entregues para negócios de estética,
terapias e psicologia no Rio Grande do Sul.

Site estático, sem build. Basta servir a pasta.

```
index.html          página inteira (HTML + CSS + JS inline)
assets/logo-mx.png  logo da marca (header + favicon)
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

## Trocar o mockup pelo print real do site

Enquanto um projeto não tem print, o card mostra um mockup de navegador com o
domínio real e as iniciais do cliente. Para usar o print de verdade, salve a
imagem em `assets/` e adicione o campo `src` no projeto:

```js
{id:'kauana', ..., src:'assets/proj-kauana.png'}
```

O card passa a exibir a imagem automaticamente, nos dois lugares (carrossel e
stack de scroll). Prints ficam melhores em ~1600×900, alinhados pelo topo.

## Antes de publicar em domínio próprio

As meta tags Open Graph no `<head>` apontam para `https://mxdigital.ia.br`.
Se o portfólio for para outro endereço, atualizar `og:url`, `og:image`,
`twitter:image` e o `<link rel="canonical">`.
