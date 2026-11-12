# 1. Instalando o Git no Mac

> ⏱️ 10 minutos · Escolha **um** dos dois caminhos.

## Já tenho o Git?

Abra o **Terminal** (aperte `Cmd + Espaço`, digite `Terminal` e dê Enter) e rode:

```bash
git --version
```

- Apareceu algo como `git version 2.39.5 (Apple Git-154)`? Já está instalado. Pule para a [criação da conta no GitHub](../02-conta-no-github.md).
- Apareceu uma janela pedindo para instalar as **ferramentas de linha de comando**? Siga o Caminho A.

---

## Caminho A: Ferramentas de linha de comando da Apple (mais simples)

O macOS traz o Git dentro de um pacote oficial da Apple chamado **Command Line Tools**. Rode no Terminal:

```bash
xcode-select --install
```

1. Vai abrir uma janela. Clique em **Instalar** e aceite a licença.
2. Aguarde o download terminar (pode levar alguns minutos).
3. Confira:

```bash
git --version
```

## Caminho B: Homebrew (para quem quer a versão mais nova)

O **Homebrew** é o instalador de programas mais usado no Mac. Se você ainda não tem, siga as instruções do site oficial: **https://brew.sh** (é um único comando para colar no Terminal).

Com o Homebrew instalado:

```bash
brew install git
```

Feche e abra o Terminal, e confira:

```bash
git --version
```

> 💡 O Homebrew costuma trazer uma versão mais recente do Git que a da Apple. Para o que vamos fazer, as duas funcionam igual.

---

## Bônus: comando `code` do VS Code

Vamos configurar o VS Code como editor do Git. Para isso, o Mac precisa conhecer o comando `code`:

1. Abra o **VS Code**.
2. Aperte `Cmd + Shift + P`.
3. Digite **Shell Command: Install 'code' command in PATH** e dê Enter.

Teste no Terminal:

```bash
code --version
```

## ✅ Checkpoint

```bash
git --version
```

Se aparecer a versão, está pronto! 🎉

## 🧠 Desafio sem IA

Descubra **onde** o Git foi instalado no seu Mac usando o comando `which git`. Ele está na mesma pasta que o do seu colega que escolheu o outro caminho?

---

[⬅️ O que é Git](../00-o-que-e-git-e-github.md) · [Próximo: Conta no GitHub ➡️](../02-conta-no-github.md)
