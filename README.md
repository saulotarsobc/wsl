# ⚡ Guia: Terminal Bonito e Produtivo com Zsh no WSL2 (Ubuntu)

> Transforme seu terminal em uma ferramenta poderosa para desenvolvimento web, com autocompletar, cores e estilo.

---

## 🚀 1. Instalar o Zsh

Atualize os pacotes e instale o Zsh:

```bash
sudo apt update
sudo apt install zsh -y
```

Verifique a instalação:

```bash
zsh --version
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
autoload -Uz compinit && compinit
zstyle ':completion:*' menu select
zstyle ':completion:*' matcher-list 'm:{a-z}={A-Za-z}'
```

Essas opções permitem:

- Autocomplete com **menu interativo**
- Completar **insensível a maiúsculas/minúsculas**

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

## 💻 Resultado Final

- Tema limpo e rápido
- Autocomplete inteligente e colorido
- Ícones e fontes bonitas
- Atalhos para desenvolvimento web (git, npm, docker…)

---

## 🧩 Exemplo Visual

_(adicione aqui um print do seu terminal personalizado!)_

---

Feito com ❤️ por [Saulo Costa](https://github.com/saulotarsobc)
