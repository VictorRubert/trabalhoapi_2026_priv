# Frequência

Explorador musical desenvolvido por Victor Luís Rubert Andriolli para Fundamentos ao Desenvolvimento Web — Sistemas de Informação — Unoesc.

**Bootstrap 5.3.8** fornece o grid responsivo, botões, formulários e utilitários. O CSS oficial e a licença MIT estão em `vendor/bootstrap/`, com integridade SHA-512 conferida contra os metadados do npm. O CSS próprio personaliza o tema e a arte do vinil. Não é necessário carregar JavaScript do Bootstrap: o diálogo de álbum é nativo do navegador.

Visual escuro com tema roxo e referências discretas a discos, fitas e grades dos anos 80 e 90.

## Executar

O projeto usa somente HTML, CSS e JavaScript, sem build ou backend. Abra pelo GitHub Pages ou use a extensão **Live Server** do VS Code para desenvolvimento local. Não precisa instalar pacotes nem configurar chaves.

É necessário acesso à internet para a Deezer, capas e fontes. Bootstrap é servido junto do site e não depende de CDN. Sem as fontes externas, a interface utiliza fontes locais.

## Funcionalidades

O site tem uma funcionalidade por endpoint: listar destaques, buscar músicas e consultar um álbum (informações e faixas). Não inclui áudio, sugestões rápidas nem paginação.

## Integração

- `GET /chart`: ranking geral sem filtros de país, artista ou gênero, com repetição de cartões. Não há seleção exclusiva de Brasil ou MPB. A Deezer ainda pode variar os dados conforme a região/IP da requisição; este endpoint não garante um ranking mundial idêntico em todos os países.
- `GET /search?q={termo}`: busca livre filtrada, limitada aos primeiros 20 resultados.
- `GET /album/{id}`: detalhes individuais e repetição de faixas.

As consultas utilizam `https://api.deezer.com` com `output=jsonp` e callback exclusivo por requisição, pois o teste da API não retornou o cabeçalho necessário para `fetch` entre origens. O carregamento por script depende da confiança na Deezer; os endpoints são fixos e os dados são inseridos com `textContent`, sem interpretar HTML retornado. Há tratamento de erro, timeout, lista vazia e respostas fora de ordem.

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
2. Buscar uma música ou artista e voltar aos destaques.
3. Buscar um termo inexistente e verificar o estado vazio.
4. Abrir uma capa, conferir informações e faixas, fechar com o botão e com Escape.
5. Testar no celular e com navegação por teclado.
6. Bloquear a rede e verificar a mensagem de erro e a opção de tentar novamente.
