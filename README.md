# Tabela do Brasileirão (local)

Projeto simples que carrega dados de `banco_jogos.csv` e exibe uma tabela de classificação.

Como usar

- Coloque o arquivo `banco_jogos.csv` na mesma pasta que o `index.html` (já existente no workspace).
- Abra `index.html` diretamente no navegador (duplo clique) ou rode um servidor estático local para evitar problemas de CORS.

Opções para rodar localmente (Windows / PowerShell):

- Abrir direto (pode falhar por CORS em alguns navegadores):

```powershell
ii .\index.html
```

- Rodar um servidor HTTP rápido com Python (recomendado):

```powershell
# Python 3.x
python -m http.server 5500
# então abra http://localhost:5500
```

- Usando Node.js com http-server (se tiver npm instalado):

```powershell
npm install --global http-server
http-server -p 5500
# então abra http://localhost:5500
```

Notas

- Se a tabela não aparecer, verifique o console do navegador (F12) e confirme que `banco_jogos.csv` foi carregado sem erros.
- O CSV esperado deve usar ponto-e-vírgula (`;`) como separador e ter um cabeçalho na primeira linha.

Nota sobre jogos restantes e deploy

- Crie um arquivo `banco_restante.csv` na mesma pasta para listar partidas que ainda não ocorreram. O site usa esse arquivo para simular resultados e incluir na classificação final.
- Para hospedar no Netlify: basta apontar para a pasta que contém `index.html` e os CSVs. Netlify serve arquivos estáticos por padrão e o fetch funcionará normalmente.
