# 🚀 Extra: conectando ao GitHub com SSH

> ⏱️ 15 minutos · Feito uma vez por computador.

> 🟡 **Etapa opcional.** Se você está começando, **pule** e volte aqui depois do seu primeiro PR. Até lá, o login pelo navegador (HTTPS) resolve tudo.

Para enviar código ao GitHub, ele precisa saber que é você. Existem dois jeitos:

| | HTTPS | SSH |
|---|---|---|
| Como funciona | Faz login pelo navegador na primeira vez | Uma "chave" fica salva no seu computador |
| Endereço do repositório | `https://github.com/...` | `git@github.com:...` |
| Para quem | Mais simples para começar | Mais usado no dia a dia profissional |

> 💡 Você já usa HTTPS desde o início da trilha. Então por que aprender SSH? Porque ele é o padrão em muitas empresas e servidores, e você vai encontrá-lo em todo lugar.

## Como funciona uma chave SSH?

Você cria um **par de chaves**:

- 🔒 **Chave privada** (`id_ed25519`): fica **só no seu computador**. Nunca envie para ninguém, nunca cole em lugar nenhum.
- 🔓 **Chave pública** (`id_ed25519.pub`): você cadastra no GitHub. Pode mostrar à vontade.

É como um cadeado e uma chave: o GitHub guarda o cadeado (pública), e só a sua chave (privada) abre.

---

## Passo 1: verificar se você já tem uma chave

**Windows (PowerShell):**
```powershell
ls $env:USERPROFILE\.ssh
```

**Mac (Terminal):**
```bash
ls ~/.ssh
```

Se aparecer `id_ed25519` e `id_ed25519.pub`, você já tem. Pule para o **Passo 3**.

## Passo 2: criar a chave

Mesmo comando no Windows e no Mac. Use o email do seu GitHub:

```bash
ssh-keygen -t ed25519 -C "seu-email@exemplo.com"
```

Ele vai perguntar três coisas:

1. **Onde salvar** (`Enter file in which to save the key`): só aperte **Enter** para usar o local padrão.
2. **Senha** (`Enter passphrase`): crie uma senha para proteger a chave (recomendado) ou aperte Enter para deixar sem.
3. **Confirmar a senha.**

> Ao digitar a senha, **nada aparece na tela**. É normal, é por segurança.

## Passo 3: deixar a chave sempre carregada

Assim você não precisa digitar a senha da chave toda hora.

### Windows (PowerShell como **administrador**)

Clique com o botão direito no PowerShell → **Executar como administrador**:

```powershell
Get-Service ssh-agent | Set-Service -StartupType Automatic
Start-Service ssh-agent
```

Depois, num PowerShell **normal**:

```powershell
ssh-add $env:USERPROFILE\.ssh\id_ed25519
```

### Mac

Crie ou edite o arquivo `~/.ssh/config`:

```bash
code ~/.ssh/config
```

Cole e salve:

```
Host github.com
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_ed25519
```

Depois adicione a chave ao agente, guardando a senha nas Chaves do Mac:

```bash
ssh-add --apple-use-keychain ~/.ssh/id_ed25519
```

## Passo 4: copiar a chave **pública**

**Windows (PowerShell):**
```powershell
Get-Content $env:USERPROFILE\.ssh\id_ed25519.pub | Set-Clipboard
```

**Mac:**
```bash
pbcopy < ~/.ssh/id_ed25519.pub
```

A chave copiada começa com `ssh-ed25519` e termina com o seu email.

> ⚠️ Confira que é o arquivo terminado em **`.pub`**. Nunca copie o arquivo sem `.pub`.

## Passo 5: cadastrar no GitHub

1. No GitHub: **foto do perfil → Settings → SSH and GPG keys**.
2. Clique em **New SSH key**.
3. **Title:** um nome para reconhecer o computador, como "Notebook Windows".
4. **Key type:** Authentication Key.
5. **Key:** cole a chave (`Ctrl+V` / `Cmd+V`).
6. Clique em **Add SSH key**.

## Passo 6: testar

```bash
ssh -T git@github.com
```

Na primeira vez, ele pergunta se você confia no servidor (`Are you sure you want to continue connecting`). Digite `yes` e Enter.

## ✅ Checkpoint

A resposta deve ser:

```
Hi seu-username! You've successfully authenticated, but GitHub does not provide shell access.
```

Esse "does not provide shell access" é normal. Deu certo! 🎉

Se aparecer `Permission denied (publickey)`, veja o [guia de problemas](../08-quando-da-errado.md#permission-denied-publickey).

## 🧠 Desafio sem IA

Abra o arquivo `id_ed25519.pub` num editor de texto e compare com a chave que aparece no GitHub em **Settings → SSH and GPG keys**. O GitHub mostra a chave inteira ou só uma "impressão digital" dela? Por que você acha que é assim?

---

Depois de configurar, troque o endereço dos seus repositórios para SSH:

```bash
git remote set-url origin git@github.com:SEU-USERNAME/NOME-DO-REPO.git
```

---

[⬅️ Início](../README.md) · [Avançado ➡️](../09-avancado.md)
