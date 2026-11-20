# Decisões

## 2026-11-19: continuar o projeto como fork

O autor original (hachi23) declarou o projeto encerrado em 2026-11-18 e convidou forks. O fork
`carbiecarbie/unicorn_overlord_pc` foi criado a partir do `main` em `f190399`, com o repositório
original como remote `upstream`.

## 2026-11-19: dados do jogo ficam fora do repositório

O dump de PS4, os arquivos de texto do Switch, saves e arquivos derivados do executável ficam
numa pasta fora do clone. Motivo: são material protegido e o projeto é público (GPL).

## 2026-11-20: integrar os PRs abertos do upstream e a correção de memória

Os PRs #116, #118 e #119 e o branch `fix/native-renderer-memory` entraram no `main` do fork por
merge, preservando a autoria. Motivo: duas revisões independentes não acharam defeito grave e o
conjunto compila e passa nos testes no Windows. O teto para o transbordo de vértices ficou para
depois de um teste jogando, porque a causa do estouro original não é conhecida.

## 2026-11-20: proteger o `main` do fork e ativar o CI

O ruleset do upstream foi aplicado ao fork e o workflow Build ficou ativo, a pedido do
mantenedor. Consequência aceita: toda mudança passa por pull request com CI verde, e cada merge
publica um pré-release `latest` público.

## 2026-11-20: o fork continua a numeração do upstream

O primeiro release do fork será a v1.7.0 (o upstream terminou na v1.6.2). MINOR sobe com recurso
novo ou mudança no renderer, PATCH só com correções. Motivo: o atualizador compara versões no
formato `vX.Y.Z` e as tags antigas vieram com o fork; recomeçar a contagem faria um release do
fork parecer mais antigo que a v1.6.2.
