# Configuração do WSL para desenvolvimento.

> Transforme seu terminal em uma ferramenta poderosa para desenvolvimento web, com autocompletar, cores e estilo.

---

## Instalação do WSL

1. Abra o PowerShell como administrador e execute:

```powershell
# Habilitar o WSL (Precisa de acesso de administrador e reiniciar o PC)
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart;
# Habilitar a Plataforma de Máquina Virtual (requerida para WSL 2)
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart;
# Baixar o kernel do WSL 2
Invoke-WebRequest -Uri https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi -OutFile wsl_update_x64.msi;
Start-Process msiexec.exe -Wait -ArgumentList '/I wsl_update_x64.msi /quiet /norestart';
# Definir o WSL 2 como padrão
wsl --set-default-version 2;
```

2. Intale o `Ubuntu-26.04`

```bash
wsl --install -d Ubuntu-26.04;
```

3. Abra o Ubuntu, crie um usuário e senha.
4. Atualize os pacotes:

```bash
sudo apt update && sudo apt upgrade -y;
```

5. Verifique a versão do WSL:

> Siga as instruções para configurar o WSL e o Ubuntu, depois volte aqui para personalizar seu terminal com Zsh e Oh My Zsh!

---

## Docker no WSL

### Instalação do Docker

Acesse [Instalar o Docker Engine no Ubuntu](https://docs.docker.com/engine/install/ubuntu/#install-using-the-convenience-script)

O Docker oferece um script de conveniência em https://get.docker.com/ para instalar o Docker em ambientes de desenvolvimento de forma não interativa. O script de conveniência não é recomendado para ambientes de produção, mas é útil para criar um script de provisionamento personalizado para suas necessidades. Consulte também as etapas de instalação usando o repositório para saber mais sobre como instalar usando o repositório de pacotes. O código-fonte do script é aberto e pode ser encontrado no docker-installrepositório no GitHub .

Sempre examine os scripts baixados da internet antes de executá-los localmente. Antes de instalar, familiarize-se com os riscos e limitações potenciais do script.

- O script requer privilégios rootde administrador sudopara ser executado.
- O script tenta detectar sua distribuição e versão do Linux e configurar seu sistema de gerenciamento de pacotes para você.
- O script não permite personalizar a maioria dos parâmetros de instalação.
- O script instala dependências e recomendações sem pedir confirmação. Isso pode instalar um grande número de pacotes, dependendo da configuração atual do seu computador.
- Por padrão, o script instala a versão estável mais recente do Docker, containerd e runc. Ao usar este script para provisionar uma máquina, isso pode resultar em atualizações inesperadas de versões principais do Docker. Sempre teste as atualizações em um ambiente de teste antes de implantá-las em seus sistemas de produção.
- O script não foi projetado para atualizar uma instalação existente do Docker. Ao usar o script para atualizar uma instalação existente, as dependências podem não ser atualizadas para a versão esperada, resultando em versões desatualizadas.

> [TIP] Visualize as etapas do script antes de executá-lo. Você pode executar o script com a opção `--dry-run` para saber quais etapas ele executará ao ser invocado:

```bash
curl -fsSL https://get.docker.com -o get-docker.sh;
sudo sh get-docker.sh;
```

### Permissões do Docker sem sudo

> Supondo que o nome do user seja `saulo`:

```bash
sudo usermod -aG docker saulo;
```

Agora, para usar o Docker sem `sudo`, faça logout e login novamente ou reinicie o terminal.

### Logar no Docker Hub

```bash
docker login;
# Basta seguir as instruções para autenticar com seu usuário do Docker Hub.
```

---

---

## 🚀 1. Instalar o Zsh

Atualize os pacotes e instale o Zsh:

```bash
sudo apt update;
sudo apt install zsh -y;
```

Verifique a instalação:

```bash
zsh --version;
```

Defina o Zsh como shell padrão:

```bash
chsh -s $(which zsh)
```

Feche e reabra o terminal para aplicar.

---

## 💎 2. Instalar o Oh My Zsh

O [Oh My Zsh](https://ohmyz.sh/) é um framework que facilita gerenciar temas e plugins no Zsh.

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

---

## 🎨 3. Escolher um Tema

Por padrão, o Oh My Zsh usa o tema **robbyrussell**.
Você pode testar outros temas editando o arquivo `~/.zshrc`:

```bash
nano ~/.zshrc
```

Procure a linha:

```properties
ZSH_THEME="robbyrussell"
```

Altere para outro tema se quiser, por exemplo:

```properties
ZSH_THEME="powerlevel10k/powerlevel10k"
```

Depois salve (`Ctrl + O`, `Enter`, `Ctrl + X`) e recarregue:

```bash
source ~/.zshrc
```

Para instalar o **Powerlevel10k** (tema avançado):

```bash
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```

---

## 🧩 4. Instalar Plugins de Autocomplete e Syntax Highlighting

Esses dois plugins deixam o terminal muito mais esperto:

```bash
# Sugestões automáticas (histórico)
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

# Destaque de sintaxe
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

Agora edite o `.zshrc`:

```bash
nano ~/.zshrc
```

Procure:

```properties
plugins=(git)
```

Troque por:

```properties
plugins=(git z npm node nvm zsh-autosuggestions zsh-syntax-highlighting)
```

Salve e recarregue:

```bash
source ~/.zshrc
```

---

## 🌈 5. Personalizar o Autocomplete

O `zsh-autosuggestions` mostra sugestões em cinza claro por padrão.
Para mudar a cor, adicione ao final do `~/.zshrc`:

```properties
# Cor das sugestões (azul-ciano suave)
ZSH_AUTOSUGGEST_HIGHLIGHT_STYLE='fg=#7dcfff'

# Estratégia de sugestão (histórico + completions)
ZSH_AUTOSUGGEST_STRATEGY=(history completion)
```

Recarregue o Zsh:

```bash
source ~/.zshrc
```

💡 Exemplos de outras cores:

```properties
ZSH_AUTOSUGGEST_HIGHLIGHT_STYLE='fg=#00ff87'  # Verde neon
ZSH_AUTOSUGGEST_HIGHLIGHT_STYLE='fg=#aaaaaa'  # Cinza claro
```

---

## ⚙️ 6. Melhorar o Sistema de Autocompletar do Zsh

Ative o menu de autocomplete com navegação pelas setas:

```bash
# Ativa o sistema de autocomplete
autoload -Uz compinit && compinit
# Ativa o menu interativo
zstyle ':completion:*' menu select
# Completar insensível a maiúsculas
zstyle ':completion:*' matcher-list 'm:{a-z}={A-Za-z}'
```

---

## 🔤 7. Instalar uma Nerd Font (para ícones)

Para exibir corretamente os ícones dos temas, instale uma **Nerd Font** no Windows:

👉 [https://www.nerdfonts.com/font-downloads](https://www.nerdfonts.com/font-downloads)

Recomendada: **MesloLGS NF** (usada pelo Powerlevel10k).

Depois, configure seu terminal (ou VSCode → Terminal → Fonte) para usar essa fonte.

---

## 🧠 8. Plugins recomendados para Dev Web

No `~/.zshrc`, você pode ativar mais plugins úteis:

```
plugins=(git z npm node nvm docker web-search)
```

- `z`: navegação rápida entre diretórios
- `npm`, `node`, `nvm`: suporte JS/Node.js
- `docker`: autocompletar comandos Docker
- `web-search`: permite pesquisar direto do terminal (`web_search google algo`)

---

## 🎯 9. Dica Final

Sempre que mudar algo no `.zshrc`, recarregue:

```bash
source ~/.zshrc
```

---

## NodeJS

## Instale o NodeJS usando o NVM (Node Version Manager):

Acesse [https://nodejs.org/en/download](https://nodejs.org/en/download) e siga as instruções para instalar o NVM no Linux.

```bash
# Download and install nvm:
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.4/install.sh | bash
# in lieu of restarting the shell
\. "$HOME/.nvm/nvm.sh"
# Download and install Node.js:
nvm install 24
# Verify the Node.js version:
node -v # Should print "v24.16.0".
# Verify npm version:
npm -v # Should print "11.13.0".
```

---

## 💻 Resultado Final

- Tema limpo e rápido
- Autocomplete inteligente e colorido
- Ícones e fontes bonitas
- Atalhos para desenvolvimento web (git, npm, docker…)

---

## Powershell

### Instalar o PowerShell no WSL

> Powershell é o terminal nativo do Windows, mas é possível personalizá-lo com temas e plugins usando o [Oh My Posh](https://ohmyposh.dev/).

Acesse [https://learn.microsoft.com/en-us/powershell/scripting/install/install-ubuntu](https://learn.microsoft.com/en-us/powershell/scripting/install/install-ubuntu) para instalar o PowerShell no WSL.

---

## Git e GitHub

### Configurar o Git

```bash
git config --global user.name "Seu Nome";
git config --global user.email "meu@email.com";
```

### Instalar o GitHub CLI

```bash
sudo apt install gh -y;
```

### Logue no GitHub CLI:

```bash
gh auth login;
# Basta seguir as instruções para autenticar via navegador.
```

---

Feito com ❤️ por [Saulo Costa](https://github.com/saulotarsobc)
