# fatec-pi-widget

Widget WordPress para exibir os Projetos Integradores em destaque no site da Fatec Itaquera.

## O que faz

Exibe cards dos projetos premiados como "Melhor PI" de cada ciclo e semestre, com o design visual do site da Fatec Itaquera (cores, tipografia e divisores do tema CPS). Cada card mostra titulo, descricao resumida, ciclo letivo, semestre do curso, orientador, tecnologias utilizadas e um link direto ao projeto no sistema original.

Os projetos sao sempre ordenados pelo mais recentemente premiado.

## Arquivos

| Arquivo | Uso |
|---|---|
| `pi-widget-wordpress-dynamic.html` | Versao recomendada. Busca os dados automaticamente via API. |
| `pi-widget-wordpress-static.html` | Versao de fallback com dados fixos no codigo. |

## Configuracao de URL

Antes de usar o widget, substitua `SUA_URL_AQUI` pela URL base do sistema de projetos implantado.

### Versao dinamica (`pi-widget-wordpress-dynamic.html`)

Localize o bloco `CONFIG` no inicio do `<script>` e altere os dois valores:

```js
var CONFIG = {
  urlSistema: 'SUA_URL_AQUI',
  urlApi:     'SUA_URL_AQUI/api/projects/recommended',
}
```

Substitua `SUA_URL_AQUI` pela URL base do sistema, sem barra no final. Exemplo:

```js
var CONFIG = {
  urlSistema: 'https://fatecitaquera.cps.sp.gov.br/',
  urlApi:     'https://fatecitaquera.cps.sp.gov.br/api/projects/recommended',
}
```

- `urlSistema` e usado no link "ver todos" e na mensagem de manutencao exibida quando a API esta indisponivel.
- `urlApi` e o endpoint que retorna os projetos em destaque em formato JSON.

### Versao estatica (`pi-widget-wordpress-static.html`)

Localize o bloco `CONFIG` no inicio do `<script>` e altere o valor:

```js
var CONFIG = {
  urlSistema: 'SUA_URL_AQUI',
}
```

Substitua `SUA_URL_AQUI` pela URL base do sistema. Exemplo:

```js
var CONFIG = {
  urlSistema: 'https://fatecitaquera.cps.sp.gov.br/',
}
```

- `urlSistema` e usado no link "ver todos" e para compor a URL de cada card no formato `urlSistema/projetos/{id}`.

## Como usar no WordPress

1. Acesse o editor da pagina no painel WordPress (editor Gutenberg)
2. Adicione um bloco **HTML Personalizado** (Custom HTML)
3. Cole o conteudo do arquivo desejado
4. Salve e publique

Nenhum plugin adicional e necessario.

## Versao dinamica (recomendada)

O arquivo `pi-widget-wordpress-dynamic.html` busca os dados do endpoint publico do sistema. O endpoint deve retornar os projetos premiados com CORS aberto para que o widget funcione a partir de qualquer dominio. Enquanto os dados carregam, um indicador de carregamento e exibido. Se a API estiver indisponivel, o widget exibe uma mensagem de manutencao com link para o sistema.

Para que a versao dinamica reflita novos projetos premiados sem precisar editar o WordPress, basta que o sistema esteja atualizado. A API e mantida no repositorio [pi-repository](https://github.com/ESTAGIO-DSM20262/pi-repository).

## Versao estatica (fallback)

O arquivo `pi-widget-wordpress-static.html` nao depende de nenhuma API. Os dados dos projetos estao fixos no codigo JavaScript do arquivo. Para adicionar ou remover projetos, edite o array `projetos` diretamente no HTML salvo no WordPress.

A ordenacao por mais recente e feita automaticamente com base no campo `ciclo` de cada projeto (formato `AAAA/S`).

## Design

O widget replica o sistema visual do site da Fatec Itaquera (tema CPS v2.0.08):

- Cores: vermelho `#b20000`, verde-petroleo `#005c6d`, ciano `#00c1cf`
- Tipografia: Roboto e Roboto Slab (Google Fonts)
- Divisor de secao em SVG, identico ao usado nas paginas do site
- Grid responsivo: 4 colunas no desktop, 2 no tablet, 1 no celular
- Hover com sombra e elevacao nos cards

## Repositorio do sistema

O codigo-fonte completo do sistema de projetos esta em:
[github.com/ESTAGIO-DSM20262/pi-repository](https://github.com/ESTAGIO-DSM20262/pi-repository)
