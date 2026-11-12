# 1. Instalando o Git no Windows

> ⏱️ 10 minutos · Escolha **um** dos dois caminhos.

## Já tenho o Git?

Abra o **PowerShell** (aperte `Win`, digite `PowerShell` e dê Enter) e rode:

```powershell
git --version
```

- Apareceu algo como `git version 2.47.1.windows.1`? Já está instalado. Pule para a [criação da conta no GitHub](../02-conta-no-github.md).
- Apareceu um erro dizendo que `git` não é reconhecido? Siga um dos caminhos abaixo.

---

## Caminho A: pelo site (recomendado para iniciantes)

1. Acesse **https://git-scm.com/downloads/win** e baixe o instalador **64-bit Git for Windows Setup**.
2. Abra o arquivo baixado. Vão aparecer várias telas. Na maioria, é só clicar em **Next**. Preste atenção nestas:

| Tela | O que escolher | Por quê |
|---|---|---|
| **Choosing the default editor used by Git** | `Use Visual Studio Code as Git's default editor` | É o editor que vamos usar. Se não tiver o VS Code, escolha `Notepad` |
| **Adjusting the name of the initial branch** | `Override the default branch name` e digite `main` | É o nome padrão do GitHub e dos nossos projetos |
| **Adjusting your PATH environment** | `Git from the command line and also from 3rd-party software` | Permite usar o Git no PowerShell e no VS Code |
| **Choosing the SSH executable** | `Use bundled OpenSSH` | Já vem pronto para usar |
| **Configuring the line ending conversions** | `Checkout Windows-style, commit Unix-style line endings` | Evita problemas de quebra de linha entre Windows e Mac |
| **Choose a credential helper** | `Git Credential Manager` | Guarda seu login do GitHub com segurança |

3. Clique em **Install** e depois em **Finish**.
4. **Feche e abra de novo** o PowerShell (ele só enxerga o Git depois disso) e confira:

```powershell
git --version
```

## Caminho B: pelo terminal (winget)

O Windows 10 e 11 já vêm com o **winget**, um instalador de programas pelo terminal. Abra o PowerShell e rode:

```powershell
winget install --id Git.Git -e --source winget
```

Depois de terminar, **feche e abra o PowerShell** e confira:

```powershell
git --version
```

> 💡 Pelo winget, o instalador usa as opções padrão. Por isso, depois você vai configurar a branch `main` e o editor manualmente no guia do [.gitconfig](../03-configuracao/gitconfig.md).

---

## Git Bash: um bônus

A instalação também traz o **Git Bash**, um terminal parecido com o do Mac e do Linux. Você pode usar tanto ele quanto o PowerShell. Nesta trilha, quando um comando for diferente entre os dois, vamos avisar.

## ✅ Checkpoint

```powershell
git --version
```

Se aparecer a versão, está pronto! 🎉

## 🧠 Desafio sem IA

Abra o **Git Bash** pelo menu Iniciar e rode `git --version` nele também. O resultado é igual ao do PowerShell?

---

[⬅️ O que é Git](../00-o-que-e-git-e-github.md) · [Próximo: Conta no GitHub ➡️](../02-conta-no-github.md)
