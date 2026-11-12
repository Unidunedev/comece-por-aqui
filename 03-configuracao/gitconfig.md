# 3.2 Turbinando o seu .gitconfig

> ⏱️ 10 minutos · Deixa o Git mais confortável e com atalhos úteis.

Todas as configurações `--global` ficam num arquivo de texto chamado **`.gitconfig`**, na sua pasta de usuário:

| Sistema | Onde fica |
|---|---|
| Windows | `C:\Users\SEU-USUARIO\.gitconfig` |
| Mac | `/Users/SEU-USUARIO/.gitconfig` |

## Abrindo o arquivo

```bash
git config --global --edit
```

Esse comando abre o arquivo no editor configurado. Se você ainda não configurou o VS Code, ele pode abrir o **Vim**, um editor no próprio terminal. Para sair do Vim sem salvar, aperte `Esc`, digite `:q!` e dê Enter. 😅

Para configurar o VS Code antes, rode:

```bash
git config --global core.editor "code --wait"
```

> No Mac, o comando `code` precisa estar instalado. Veja o [bônus da instalação](../01-instalacao/mac.md#bônus-comando-code-do-vs-code).

## O .gitconfig da Unidunedev

Copie, cole no arquivo, **troque nome e email** e salve:

```properties
[user]
	name = Seu Nome
	email = 123456+seu-username@users.noreply.github.com
[init]
	defaultBranch = main
[core]
	editor = code --wait
[pull]
	rebase = false
[alias]
	s = !git status -s
	c = !git add . && git commit -m
	amend = !git add . && git commit --amend --no-edit
	l = !git log --pretty=format:'%C(blue)%h%C(red)%d %C(white)%s %C(cyan)[%cn] %C(green)%cr'
```

## Linha por linha

### `[user]`
Seu nome e email, os mesmos da [etapa anterior](identidade.md).

### `[init] defaultBranch = main`
Todo repositório novo começa com uma branch principal. O GitHub e os nossos projetos chamam ela de **`main`**. Versões antigas do Git usavam `master`. Usando `main` em todo lugar, você evita confusão.

### `[core] editor = code --wait`
Quando o Git precisar que você escreva algo (como uma mensagem de commit mais longa), ele abre o VS Code. O `--wait` faz o Git esperar você **fechar a aba** antes de continuar.

### `[pull] rebase = false`
Define o comportamento padrão do `git pull`. Sem isso, versões recentes do Git mostram um aviso no primeiro pull. Vamos entender a diferença no [guia avançado](../09-avancado.md#rebase).

### `[alias]`: atalhos
Um **alias** é um apelido para um comando maior. O `!` no começo significa "rode isso como comando do terminal".

| Você digita | O Git roda | Para quê |
|---|---|---|
| `git s` | `git status -s` | Ver o que mudou, em formato curto |
| `git c "mensagem"` | `git add .` + `git commit -m "mensagem"` | Adicionar **tudo** e commitar de uma vez |
| `git amend` | `git add .` + `git commit --amend --no-edit` | Colocar mudanças esquecidas no **último** commit |
| `git l` | `git log` colorido e em uma linha | Ver o histórico de forma bonita |

> ⚠️ **Use os atalhos depois de entender os comandos de verdade.** Primeiro aprenda o `git add` e o `git commit` no [guia de primeiros comandos](../04-primeiros-comandos.md). O `git c` adiciona **todos** os arquivos, inclusive os que você talvez não quisesse.
>
> ⚠️ **`git amend` reescreve o último commit.** Só use se ele **ainda não foi enviado** para o GitHub (`git push`).

### Como fica o `git l`

```
a1b2c3d (HEAD -> main, origin/main) Adiciona meu card no mural [Ana Souza] 2 hours ago
e4f5g6h Corrige texto do botão [João Lima] 1 day ago
```

- 🔵 **azul:** o código curto do commit
- 🔴 **vermelho:** branches e etiquetas apontando para ele
- ⚪ **branco:** a mensagem
- 🩵 **ciano:** quem fez
- 🟢 **verde:** há quanto tempo

## Só no Windows: quebras de linha

Windows e Mac salvam o "fim de linha" dos arquivos de jeitos diferentes. Se você instalou pelo site com a opção recomendada, já está resolvido. Se instalou pelo winget, rode:

```powershell
git config --global core.autocrlf true
```

## ✅ Checkpoint

```bash
git config --global --list
```

Deve aparecer `init.defaultbranch=main`, `core.editor=code --wait` e os quatro `alias.*`.

## 🧠 Desafio sem IA

Crie um alias seu: `git hoje`, que mostra só os commits das últimas 24 horas. Dica: procure na documentação do `git log` pela opção `--since`.

---

[⬅️ Identidade](identidade.md) · [Próximo: Chave SSH ➡️](ssh.md)
