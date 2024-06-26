# Como instalar/configurar para exibir somente a última pasta no terminal no `Linux Ubuntu`

## Resumo

Neste documento estão contidos os principais comandos e configurações para instalar/configurar para mostrar somente a última pasta no terminal no `Linux Ubuntu`.

## _Abstract_

_This document contains the main commands and settings to install/configure to show only the last folder in the terminal in `Linux Ubuntu`._


## Revisão(ões)/Versão(ões)

| Revisão número | Data da revisão | Descrição da revisão                                    | Autor da revisão                                |
|:--------------:|:---------------:|:--------------------------------------------------------|:------------------------------------------------|
| 0              | 24/10/2023      | <ul><li>Revisão inicial/criação do documento.</li></ul> | <ul><li>Eden Denis F. da S. L. Santos</li></ul> |
| 1              | 14/11/2023      | <ul><li>Incluída a descrição.</li></ul>                 | <ul><>liEden Denis F. da S. L. Santos</li></ul> |


## Controle de configuração/instalação nos Sistemas Operacionais (SO) vs. Computador

|Numero|Computador         |Sistema Operacional (SO)|Status da configuração/instalação|
|:----:|:-----------------:|:----------------------:|:-------------------------------:|
|1     |Dell Precision 7520|Kali   Linux            |OK                               |
|2     |Dell Precision 7520|Linux Ubuntu            |N/A                              |
|3     |Dell Precision 7520|Linux Xubuntu           |OK                               |
|4     |Dell Precision 7520|Windows                 |Pendente                         |
|5     |Asus               |Kali   Linux            |N/A                              |
|6     |Asus               |Linux Ubuntu            |Pendente                         |
|7     |Asus               |Linux Xubuntu           |Pendente                         |
|8     |Asus               |Windows                 |Pendente                         |


## Descrição

### `shell`

Um "shell" é uma interface de linha de comando que permite aos usuários interagirem com um sistema operacional ou software por meio de comandos de texto. Ele atua como uma camada intermediária entre o usuário e o núcleo do sistema operacional, permitindo a execução de tarefas, manipulação de arquivos, gerenciamento de processos e configuração do sistema. Os shells são comumente encontrados em sistemas Unix-like, como o Linux, e também estão disponíveis em outros sistemas operacionais, como o Windows. Eles podem variar em complexidade e recursos, desde shells simples que fornecem apenas funcionalidades básicas até shells avançados, como o Bash, o PowerShell e o Zsh, que oferecem automação avançada, scripting e recursos de personalização. Os shells desempenham um papel fundamental na automação de tarefas, na administração de sistemas e na programação de scripts, tornando-se uma ferramenta essencial para administradores de sistemas, desenvolvedores e usuários avançados.


## 1. Configurar/Instalar para exibir somente a última pasta no terminal do Linux [1]

Para fazer com que o terminal do Linux mostre apenas o nome da última pasta (ao invés do caminho completo), você precisa modificar o arquivo de configuração do `shell` que você está usando. Para o `bash`, este arquivo é geralmente `~/.bashrc`. Para o `zsh`, é `~/.zshrc`.

Vou mostrar como fazer isso para o `bash`, mas o processo é similar para outros shells.

1. Abra o terminal. Você pode fazer isso pressionando: `Ctrl + Alt + T`


2. Certifique-se de que seu sistema esteja limpo e atualizado.

    2.1 Remover pacotes `.deb` antigos ou duplicados do cache local. É útil para liberar espaço, pois remove apenas os pacotes que não podem mais ser baixados (ou seja, versões antigas de pacotes que foram atualizados). Digite o seguinte comando: `sudo apt autoclean`

    2.2 Remover pacotes que foram automaticamente instalados para satisfazer as dependências de outros pacotes e que não são mais necessários. Digite o seguinte comando: `sudo apt autoremove -y`

    2.3 Buscar as atualizações disponíveis para os pacotes que estão instalados em seu sistema. Digite o seguinte comando e pressione `Enter`: `sudo apt update -y`

    2.4 Para ver a lista de pacotes a serem atualizados, digite o seguinte comando e pressione `Enter`:  `sudo apt list --upgradable`

    2.5 Realmente atualizar os pacotes instalados para as suas versões mais recentes, com base na última vez que você executou `sudo apt update -y`. Digite o seguinte comando e pressione `Enter`: `sudo apt full-upgrade -y`

    2.6 Remover pacotes que foram automaticamente instalados para satisfazer as dependências de outros pacotes e que não são mais necessários. Digite o seguinte comando: `sudo apt autoremove -y`

    2.7 Remover pacotes `.deb` antigos ou duplicados do cache local. É útil para liberar espaço, pois remove apenas os pacotes que não podem mais ser baixados (ou seja, versões antigas de pacotes que foram atualizados). Digite o seguinte comando: `sudo apt autoclean`

3. Abra o arquivo `~/.bashrc` em um editor de texto. Você pode fazer isso diretamente do terminal: `sudo nano ~/.bashrc`

4. Encontre as linhas que define os `PS1`, que é o `prompt` do `shell`. As linhas podes se parecer com: `PS1='${debian_chroot:+($debian_chroot)}\u@\h:\w\$ '`

    Veja o exemplo do código inteiro abaixo, perceber que, neste caso, existem 3 (três) linhas a serem alteradas como segue no próximo Item:

    ```
    if [ "$color_prompt" = yes ]; then
        PS1='${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\W>
    else
        PS1='${debian_chroot:+($debian_chroot)}\u@\h:\W\$ '
    fi
    unset color_prompt force_color_prompt

    # If this is an xterm set the title to user@host:dir
    case "$TERM" in
    xterm*|rxvt*)
        PS1="\[\e]0;${debian_chroot:+($debian_chroot)}\u@\h: \W\a\]$PS1"
        ;;
    *)
        ;;
    esac
    ```

5. Modifique esta linha para mostrar apenas o nome da última pasta. Uma forma de fazer isso é: `PS1='${debian_chroot:+($debian_chroot)}\u@\h:\W\$ '`

Aqui, `\W` faz com que apenas o nome da última pasta seja exibido.

6. Depois de fazer a alteração, salve o arquivo e saia do editor:

6.1 **Salvar o arquivo:** Pressione para salvar as mudanças: `Ctrl + O`. 

Isso abrirá uma linha na parte inferior do editor perguntando o nome do arquivo para salvar. 

6.2 Se você deseja manter o mesmo nome, simplesmente pressione `Enter`.

6.3 **Sair do nano:** Para sair do editor nano após salvar o arquivo, pressione: `Ctrl + X`

7. Aplique as mudanças com o comando: `source ~/.bashrc`

Agora, seu prompt do terminal deve mostrar apenas o nome da última pasta.

### 1.1 Explicação dos códigos

- **`nano ~/.bashrc`:** Abre o arquivo de configuração `.bashrc` usando o editor de texto nano.

- **`PS1='${debian_chroot:+($debian_chroot)}\u@\h:\w\$ '`:** Esta é uma linha típica que você encontrará no arquivo .bashrc. Ela configura a aparência do prompt do terminal.

    - **`\u`:** Nome do usuário

    - **`\h:`** Nome do host

    - **`\w:`** Caminho completo do diretório atual

    - **`\$:`** Símbolo do prompt (geralmente $ para usuários normais e # para o root)

- **`PS1='${debian_chroot:+($debian_chroot)}\u@\h:\W\$ '`:** Modificamos \w para \W para mostrar apenas o nome do último diretório.

    - **`source ~/.bashrc`:** Este comando aplica as alterações feitas no arquivo .bashrc sem a necessidade de reiniciar o terminal.

Isso deve resolver o seu problema!


## 2. Código completo para configurar/instalar

Para instalar o `Telegram Desktop` no `Linux Ubuntu` sem precisar digitar linha por linha, você pode seguir estas etapas:

1. Abra o terminal. Você pode fazer isso pressionando: `Ctrl + Alt + T`

2. Digite o seguinte comando e pressione `Enter`:

    ```
    **NÃO** há.
    ```

## Referências

[1] OPENAI. ***Exibir nome da pasta.:*** https://chat.openai.com/c/6f1089c0-b7c9-4e65-a481-be2cb145bb46 (texto adaptado). Acessado em: 24/10/2023 16:46.

[2] OPENAI. ***Vs code: editor popular:*** https://chat.openai.com/c/b640a25d-f8e3-4922-8a3b-ed74a2657e42 (texto adaptado). ChatGPT. Acessado em: 06/02/2024 09:28.

