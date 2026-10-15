# Frequência

Explorador musical com foco editorial em MPB, desenvolvido por Victor Luís Rubert Andriolli para Fundamentos ao Desenvolvimento Web — Sistemas de Informação — Unoesc.

## Executar

Não precisa instalar dependências ou configurar chaves. Na pasta do projeto:

```sh
python3 -m http.server 8000
```

Abra a página servida pelo Python no navegador. É necessário acesso à internet para os dados da Deezer, capas, prévias e fontes. Sem as fontes externas, a interface utiliza fontes locais.

## Integração

- `GET /chart`: ranking geral sem filtros, disponível na aba **Ranking geral Deezer**, com repetição de cartões.
- `GET /search?q={termo}`: busca filtrada, com paginação. Na página inicial, buscas por `artist:"Djavan"`, `artist:"Marisa Monte"`, `artist:"Milton Nascimento"` e `artist:"Gilberto Gil"` compõem a seleção MPB, intercalada e sem IDs de faixas repetidos. A seleção é editorial e não um ranking do gênero; a busca digitada continua livre.
- `GET /album/{id}`: detalhes individuais e repetição de faixas.

As consultas utilizam `https://api.deezer.com` com `output=jsonp` e callback exclusivo por requisição, pois o teste da API não retornou o cabeçalho necessário para `fetch` entre origens. O carregamento por script depende da confiança na Deezer; os endpoints são fixos e os dados são inseridos com `textContent`, sem interpretar HTML retornado. Há tratamento de erro, timeout, lista vazia e respostas fora de ordem. Prévias dependem da disponibilidade da faixa e podem expirar.

## GitHub Pages

Envie os arquivos para o repositório. Em **Settings → Pages**, configure **Deploy from a branch**, selecione a branch com os arquivos e a pasta **/ (root)**. Os caminhos relativos permitem hospedar em um subdiretório. Caso a disciplina exija a branch `gh-pages`, publique os mesmos arquivos nela e selecione essa branch nas configurações.

A disponibilidade do Pages para repositórios privados depende do plano da conta. Não é necessário disponibilizar credenciais no código.

## Conferência manual

1. Abrir a página, verificar a seleção MPB, alternar para o ranking geral e retornar à seleção.
2. Buscar um artista, carregar mais resultados e voltar aos destaques.
3. Buscar um termo inexistente e verificar o estado vazio.
4. Abrir uma capa, conferir informações e faixas, fechar com o botão e com Escape.
5. Reproduzir uma prévia disponível e fechar o reprodutor.
6. Testar no celular e com navegação por teclado.
7. Bloquear a rede e verificar a mensagem de erro e a opção de tentar novamente.
