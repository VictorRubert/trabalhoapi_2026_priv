# Frequência

Explorador musical desenvolvido por Victor Luís Rubert Andriolli para Fundamentos ao Desenvolvimento Web — Sistemas de Informação — Unoesc.

Visual escuro com tema roxo e referências discretas a discos, fitas e grades dos anos 80 e 90.

## Executar

Não precisa instalar dependências ou configurar chaves. Na pasta do projeto:

```sh
python3 -m http.server 8000
```

Abra a página servida pelo Python no navegador. É necessário acesso à internet para os dados da Deezer, capas, prévias e fontes. Sem as fontes externas, a interface utiliza fontes locais.

## Integração

- `GET /chart`: ranking geral sem filtros, com repetição de cartões.
- `GET /search?q={termo}`: busca livre filtrada, com paginação.
- `GET /album/{id}`: detalhes individuais e repetição de faixas.

As consultas utilizam `https://api.deezer.com` com `output=jsonp` e callback exclusivo por requisição, pois o teste da API não retornou o cabeçalho necessário para `fetch` entre origens. O carregamento por script depende da confiança na Deezer; os endpoints são fixos e os dados são inseridos com `textContent`, sem interpretar HTML retornado. Há tratamento de erro, timeout, lista vazia e respostas fora de ordem. Prévias dependem da disponibilidade da faixa e podem expirar.

## GitHub Pages

A branch `gh-pages` contém o site estático completo, incluindo `.nojekyll`. No GitHub, abra **Settings → Pages** e configure:

- **Source:** Deploy from a branch
- **Branch:** gh-pages
- **Folder:** / (root)

Clique em **Save** e acompanhe o deploy na aba **Actions**. Após a publicação, o endereço esperado é `https://victorrubert.github.io/trabalhoapi_2026_priv/`.

O site não precisa de Node, build ou backend. CSS e JavaScript usam caminhos relativos, e as chamadas públicas à Deezer usam HTTPS/JSONP. Para atualizar a publicação após mudanças na `main`, atualize também a branch `gh-pages`:

```sh
git push origin HEAD:gh-pages
```

Execute esse comando a partir do commit que deseja publicar.

A disponibilidade do Pages para repositórios privados depende do plano da conta. Não é necessário disponibilizar credenciais no código.

## Conferência manual

1. Abrir a página e verificar o ranking geral.
2. Buscar um artista, carregar mais resultados e voltar aos destaques.
3. Buscar um termo inexistente e verificar o estado vazio.
4. Abrir uma capa, conferir informações e faixas, fechar com o botão e com Escape.
5. Reproduzir uma prévia disponível e fechar o reprodutor.
6. Testar no celular e com navegação por teclado.
7. Bloquear a rede e verificar a mensagem de erro e a opção de tentar novamente.
