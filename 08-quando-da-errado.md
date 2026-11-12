# 8. Quando dá errado (e vai dar, faz parte!)

> 📖 Guia de consulta. Volte aqui sempre que travar.

Primeira regra: **calma, quase tudo no Git tem volta.** Antes de qualquer coisa, rode `git status`. Ele quase sempre diz o que está acontecendo e até sugere o comando para resolver.

## Índice

- [Desfazer mudanças num arquivo (antes do add)](#desfazer-mudanças-num-arquivo-antes-do-add)
- [Tirar um arquivo da área de preparo](#tirar-um-arquivo-da-área-de-preparo)
- [Errei a mensagem do último commit](#errei-a-mensagem-do-último-commit)
- [Esqueci um arquivo no último commit](#esqueci-um-arquivo-no-último-commit)
- [Quero desfazer o último commit](#quero-desfazer-o-último-commit)
- [Commitei na branch errada](#commitei-na-branch-errada)
- [Conflito de merge](#conflito-de-merge)
- [Push rejeitado](#push-rejeitado-rejected--non-fast-forward)
- [Permission denied (publickey)](#permission-denied-publickey)
- [Detached HEAD](#detached-head)
- [Fiquei preso numa tela estranha](#fiquei-preso-numa-tela-estranha)
- [Apaguei algo importante](#apaguei-algo-importante)

---

## Desfazer mudanças num arquivo (antes do add)

Mexeu num arquivo e quer voltar como estava no último commit:

```bash
git restore nome-do-arquivo
```

> ⚠️ As mudanças não salvas nesse arquivo são **perdidas**.

## Tirar um arquivo da área de preparo

Deu `git add` sem querer? Ele volta para a área de trabalho, sem perder nada:

```bash
git restore --staged nome-do-arquivo
```

## Errei a mensagem do último commit

```bash
git commit --amend -m "Mensagem certa"
```

> ⚠️ Só se ainda **não deu push**. Reescrever commits já enviados atrapalha quem já baixou.

## Esqueci um arquivo no último commit

```bash
git add arquivo-esquecido
git commit --amend --no-edit
```

Ou o atalho do nosso [.gitconfig](03-configuracao/gitconfig.md): `git amend`. Mesmo aviso: só antes do push.

## Quero desfazer o último commit

**Mantendo as mudanças** nos arquivos (o mais comum):

```bash
git reset --soft HEAD~1
```

O commit some, mas os arquivos continuam do jeito que estavam, prontos para um novo commit.

**Já deu push?** Não use `reset`. Use `revert`, que cria um commit novo que desfaz o anterior, sem reescrever a história:

```bash
git revert HEAD
```

## Commitei na branch errada

Fez commits na `main` que deveriam estar numa branch? Se **ainda não deu push**:

```bash
git switch -c feat/nome-certo   # cria a branch nova com os commits
git switch main
git reset --hard origin/main    # volta a main para como está no GitHub
```

> ⚠️ O `reset --hard` descarta tudo o que não estiver commitado. Confira com `git status` antes.

## Conflito de merge

Acontece quando duas branches mudam **a mesma linha**. O Git marca o arquivo assim:

```
<<<<<<< HEAD
Meu hobby é programar.
=======
Meu hobby é jogar videogame.
>>>>>>> feat/hobbies
```

- Entre `<<<<<<< HEAD` e `=======`: a versão da **sua branch atual**.
- Entre `=======` e `>>>>>>>`: a versão que está **chegando**.

**Para resolver:**

1. Abra o arquivo (o VS Code mostra botões: *Accept Current*, *Accept Incoming*, *Accept Both*).
2. Deixe o texto do jeito que deve ficar e **apague as marcações** `<<<<<<<`, `=======` e `>>>>>>>`.
3. Salve e finalize:

```bash
git add nome-do-arquivo
git commit
```

Quer desistir do merge e voltar como estava?

```bash
git merge --abort
```

## Push rejeitado (`rejected` / `non-fast-forward`)

```
! [rejected]        main -> main (fetch first)
```

O GitHub tem commits que você ainda não tem. Busque primeiro e envie de novo:

```bash
git pull
git push
```

Se aparecer conflito no `pull`, resolva como explicado acima.

## Permission denied (publickey)

O GitHub não reconheceu sua chave SSH. Confira:

1. `ssh -T git@github.com` funciona? Se não, refaça o [guia de SSH](03-configuracao/ssh.md).
2. A chave **pública** (`.pub`) está cadastrada no GitHub?
3. O agente tem a chave carregada? Rode `ssh-add -l`. Se não listar nada, rode o `ssh-add` do guia de novo.
4. Plano B: use o endereço **HTTPS** do repositório.

## Detached HEAD

```
You are in 'detached HEAD' state.
```

Você "entrou" num commit antigo em vez de estar numa branch. Para voltar:

```bash
git switch main
```

Fez commits nesse estado e quer guardá-los? Crie uma branch antes de sair:

```bash
git switch -c resgate
```

## Fiquei preso numa tela estranha

| A tela | Como sair |
|---|---|
| Lista longa com `:` ou `(END)` no final (`git log`, `git diff`) | Aperte `q` |
| Editor **Vim** (tela preta, `~` nas linhas) | `Esc`, digite `:wq` e Enter para salvar e sair, ou `:q!` para sair sem salvar |
| Editor **nano** (atalhos `^X` embaixo) | `Ctrl + X`, depois `Y` e Enter |

Dica: configure o VS Code como editor no [.gitconfig](03-configuracao/gitconfig.md) para não cair mais no Vim.

## Apaguei algo importante

O Git guarda um registro de **tudo** o que o `HEAD` fez nos últimos meses, até commits "apagados":

```bash
git reflog
```

Encontre o commit que você quer recuperar e crie uma branch nele:

```bash
git switch -c recuperado a1b2c3d
```

Mais detalhes no [guia avançado](09-avancado.md#reflog-a-rede-de-segurança).

---

## Nada disso resolveu?

1. Leia a mensagem de erro com calma. Ela geralmente diz o problema.
2. Pesquise a mensagem exata.
3. Pergunte no grupo da comunidade, mandando **o comando que rodou** e **a mensagem de erro completa** (print ou texto).

---

[⬅️ Fork e Pull Request](07-fork-e-pull-request.md) · [Próximo: Avançado ➡️](09-avancado.md)
