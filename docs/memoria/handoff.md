# Handoff

Atualizado em 2026-11-20.

## O que a última sessão fez

- Criou o fork, clonou com os submódulos e adicionou o remote `upstream`.
- Criou `AGENTS.md`, `CLAUDE.md` e `docs/memoria/`, direto no `main` do fork.
- Instalou os pacotes CLANG64 no MSYS2 (`C:\msys64`), compilou o `main` e rodou os testes: tudo
  passou (detalhes em `estado.md`).
- Iniciou o jogo a partir do código por 55 s (RTX 5080): sem erros no log.
- Revisou e integrou no `main` os PRs #116, #118 e #119 do upstream e o branch de memória do
  renderer, com três ajustes do fork (ver `estado.md` e `decisoes.md`).
- Aplicou o ruleset "Protect main", ativou o workflow Build e fez o merge do PR #1 do fork
  (notas do pré-release e passo de publicação). O pré-release `latest` do fork foi publicado
  pela primeira vez, com os jobs `Linux`, `Windows` e `Publish` verdes.

## Ambiente local

- Build: `bash build.sh` no shell MSYS2 CLANG64, ou de fora dele com `MSYSTEM=CLANG64` e
  `C:\msys64\usr\bin\bash.exe -lc`. Leva cerca de 12 s.
- Testes nativos no build de desenvolvimento: os alvos `*-test` do CMake em `out/gpu`
  (`packaging/test-native.sh` espera `out/gpu-static`, do build `--static`).
- Pacote para Windows: o `packaging/deps.sh` recusa caminhos com espaço, e o clone fica em
  `Unicorn Overlord\`. Use um worktree sem espaços (`D:\Projetos\uo-pkg`, que já tem as
  bibliotecas estáticas compiladas em `out/deps`). Lá: `bash packaging/windows/build.sh unicorn`
  no CLANG64 e depois, num shell normal com `C:\msys64\clang64\bin` no `PATH`,
  `py -3 packaging/package.py unicorn` (o `py` não é visto de dentro do MSYS2). Sai em `dist/`.
- O `curl` do MSYS2 falhou na verificação de certificado ao baixar as fontes. Elas foram baixadas
  com o `curl` do Windows para `out/deps/src` e conferidas pelo SHA-256 fixado no `deps.sh`.
- Rodar: `VW_GAME_DIR=<dump> VW_DATA_DIR=run_uo py -3 run.py`. `run_uo/` está no `.gitignore`.
- A instalação de jogo para testes fica ao lado do clone, em
  `..\Unicorn.Overlord-game\Unicorn.Overlord-P2P` (programa v1.6.2 empacotado). O dump está em
  `data\game` (CUSA36381 v01.04 com o patch de inglês) e o texto oficial do Switch 1.05 em
  `data\languages\Unicorn_US.CPK`.
- `run_uo` não tem a pasta `languages`: rodando do código, o inglês vem do patch. Para usar o
  texto do Switch, copie o `Unicorn_US.CPK` para `run_uo\languages` ou defina `VW_LANGUAGES_DIR`.

## Pendências

- O `main` do fork está protegido pelo ruleset "Protect main" (`.github/main-protection.json`,
  aplicado em 2026-11-20): nada entra por push direto, nem do dono. Toda mudança, inclusive a
  memória do projeto, vai por pull request com os checks `Linux` e `Windows` verdes e o branch
  atualizado com o `main`. Para desfazer: Settings > Rules > Rulesets no GitHub, ou
  `gh api -X DELETE repos/carbiecarbie/unicorn_overlord_pc/rulesets/<id>`.
- O workflow Build está ativo no fork. Cada merge no `main` publica o pré-release `latest` do
  fork (binários públicos). O job de Linux, que no upstream falhava na instalação do toolchain
  (erro 503 do PPA), passa no fork.
- A tag `latest` veio do upstream com o fork, e na primeira publicação o release ficou preso ao
  commit antigo dela; foi movida à mão para o commit do merge. Nos próximos merges o workflow
  apaga e recria a tag sozinho, porque já existe um release do fork.
- Use `gh` sempre com `--repo carbiecarbie/unicorn_overlord_pc`: sem isso ele consulta o
  upstream, cujo PR #1 é outro.
- Ninguém baixou nem jogou o pacote do `latest` do fork.
- O atualizador do launcher agora consulta os releases do fork (`scripts/updates.py`,
  `REPOSITORY`), que ainda não tem nenhum, então não oferece nada. Antes oferecia a v1.6.2 do
  upstream a qualquer build do fork, porque a versão `latest-N-g<hash>` conta como mais antiga
  que todo release. Os links do pacote (`SOURCE.txt`, `README.txt`) e do modelo de issue também
  apontam para o fork.
- Esquema de versões (em `docs/RELEASING.md`): o fork continua a numeração do upstream, e o
  primeiro release será a v1.7.0. Nenhum release foi publicado; o `README.md` diz isso e aponta
  a v1.6.2 do upstream como último build lançado.
- O pacote do fork não inclui o renderer shadPS4 (o oficial inclui os dois); isso depende do
  branch `shadps4-edition`.
- Na execução de teste as telas iniciais ficaram em cerca de 33 FPS com a janela sem foco; não
  foi investigado se é o jogo (telas de logo) ou limitação com a janela em segundo plano.

## Próximos passos sugeridos

1. Jogar além do capítulo 1 com `VW_FRAME_STATS=1` e anotar as linhas `Native:` do log; conferir
   na tela o Fit, o Stretch e o mouse no mapa de batalha.
2. Fazer uma sessão longa (mais de 90 minutos) para exercitar a correção de memória.
3. Depois de jogar um build do CI, publicar a v1.7.0 seguindo `docs/RELEASING.md`.
