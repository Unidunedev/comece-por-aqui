# 3.1 Dizendo ao Git quem você é

> ⏱️ 5 minutos · Funciona igual no Windows (PowerShell ou Git Bash) e no Mac (Terminal).

Todo commit fica "assinado" com um **nome** e um **email**. É assim que o GitHub sabe que o commit é seu e mostra os quadradinhos verdes no seu perfil.

## Configurando

Troque pelos seus dados e rode:

```bash
git config --global user.name "Seu Nome"
git config --global user.email "123456+seu-username@users.noreply.github.com"
```

- **`--global`** significa "vale para todos os projetos deste computador".
- No email, use o **email `noreply`** que você copiou na [etapa anterior](../02-conta-no-github.md#proteja-seu-email). Se usar outro email, ele precisa estar cadastrado na sua conta do GitHub, senão os commits não aparecem no seu perfil.

## Conferindo

```bash
git config --global user.name
git config --global user.email
```

Ou veja tudo de uma vez:

```bash
git config --global --list
```

## E se eu errar?

É só rodar o comando de novo com o valor certo. Ele substitui o anterior.

## ✅ Checkpoint

O comando `git config --global --list` mostra `user.name` e `user.email` com os seus dados.

## 🧠 Desafio sem IA

O Git também aceita configurações **só para um projeto** (sem o `--global`). Em que situação isso seria útil? Dica: pense em quem usa o mesmo computador para a faculdade e para o trabalho.

---

[⬅️ Conta no GitHub](../02-conta-no-github.md) · [Próximo: Turbinando o .gitconfig ➡️](gitconfig.md)
