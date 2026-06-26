# Servidor Minecraft Fabric no GitHub Codespaces

Este tutorial ensina a criar um servidor de Minecraft Java com Fabric utilizando:

* GitHub Codespaces
* Crafty Controller
* Fabric Loader
* Fabric API
* Playit.gg
* Docker

O Crafty Controller será utilizado para administrar o servidor, enquanto o Playit.gg criará um endereço público para que outras pessoas possam entrar.

---

# Parte 1 — Instalando o Crafty Controller

## 1. Criar e abrir o Codespace

Depois de criar o repositório no GitHub:

1. Abra o repositório.
2. Clique em **Code**.
3. Entre na aba **Codespaces**.
4. Clique em **Create codespace on main**.
5. Aguarde o ambiente carregar.

Quando o Codespace abrir, utilize o terminal localizado na parte inferior da tela.

---

## 2. Preparar o ambiente

Execute:

```bash
sudo apt update && sudo apt upgrade && sudo apt install git
```

Esse comando atualiza os pacotes do ambiente e instala o Git, necessário para baixar o instalador do Crafty.

Quando o terminal perguntar se deseja continuar, digite:

```text
Y
```

e pressione **Enter**.

### Configuração do OpenSSH

Durante a atualização, poderá aparecer uma tela chamada:

```text
Configuring openssh-server
```

Mantenha selecionada a opção:

```text
keep the local version currently installed
```

Depois, pressione **Enter** para confirmar.

Essa escolha preserva as configurações utilizadas pelo GitHub Codespaces.

---

## 3. Limpar o terminal

Depois que a atualização terminar, execute:

```bash
clear
```

Esse comando apenas limpa visualmente o terminal.

---

## 4. Instalar a dependência `distro`

Execute:

```bash
pip install distro
```

O pacote `distro` permite que o instalador identifique corretamente o sistema Linux utilizado pelo Codespace.

Caso o instalador não encontre o módulo, execute:

```bash
sudo python3 -m pip install distro --break-system-packages
```

---

## 5. Baixar o instalador do Crafty

Execute:

```bash
git clone https://gitlab.com/crafty-controller/crafty-installer-4.0.git
```

Esse comando criará a pasta:

```text
crafty-installer-4.0
```

com os arquivos necessários para a instalação.

---

## 6. Entrar na pasta do instalador

Execute:

```bash
cd crafty-installer-4.0
```

---

## 7. Iniciar a instalação

Execute:

```bash
sudo ./install_crafty.sh
```

O instalador começará a preparar o Crafty Controller e fará algumas perguntas.

---

## 8. Confirmar a instalação no Ubuntu

Quando aparecer uma pergunta semelhante a:

```text
Would you like to continue installing Crafty on Ubuntu?
```

Digite:

```text
Y
```

e pressione **Enter**.

---

## 9. Recusar o diretório padrão

Quando aparecer:

```text
Install Crafty to this directory? /var/opt/minecraft/crafty - ['y', 'n']:
```

Digite:

```text
N
```

e pressione **Enter**.

Vamos instalar o Crafty dentro da pasta do próprio Codespace.

---

## 10. Escolher a pasta de instalação

O instalador perguntará onde o Crafty deverá ser instalado.

No explorador de arquivos do Codespace:

1. Localize o arquivo `README.md`.
2. Clique nele com o botão direito.
3. Selecione **Copy Path** ou **Copiar Caminho**.
4. Cole o caminho no terminal.

O caminho será parecido com:

```text
/workspaces/nome-do-repositorio/README.md
```

Apague somente:

```text
README.md
```

e substitua por:

```text
Minecraft
```

O resultado deverá ficar assim:

```text
/workspaces/nome-do-repositorio/Minecraft
```

Pressione **Enter**.

---

## 11. Escolher a branch do Crafty

Quando aparecer:

```text
Which branch of Crafty would you like to run? - ['master', 'dev']: master
```

Mantenha:

```text
master
```

e pressione **Enter**.

---

## 12. Não criar um arquivo de serviço

Quando aparecer:

```text
Would you like to make a service file for Crafty? - ['y', 'n']:
```

Digite:

```text
N
```

e pressione **Enter**.

No Codespaces, o Crafty será iniciado manualmente.

---

## 13. Iniciar o Crafty Controller

Depois que a instalação terminar, execute:

```bash
/workspaces/nome-do-repositorio/Minecraft/run_crafty.sh
```

Exemplo:

```bash
/workspaces/minecraft-fabric-server-codespaces/Minecraft/run_crafty.sh
```

Substitua `nome-do-repositorio` pelo nome exato do seu repositório.

Outra opção é:

1. Abrir a pasta `Minecraft`.
2. Localizar `run_crafty.sh`.
3. Clicar com o botão direito.
4. Selecionar **Copy Path**.
5. Colar o caminho no terminal.
6. Pressionar **Enter**.

Não feche esse terminal enquanto estiver utilizando o Crafty.

---

## 14. Abrir o painel no navegador

Com o Crafty em execução:

1. Abra a aba **Portas** ou **Ports**.
2. Localize a porta utilizada pelo Crafty.
3. Clique no endereço encaminhado.
4. O painel será aberto em uma nova aba.

---

# Parte 2 — Primeiro acesso ao Crafty

## 15. Encontrar as credenciais iniciais

Na tela de login, clique em:

```text
Forgot Password
```

ou:

```text
Esqueci a senha
```

Volte ao terminal em que o Crafty está sendo executado.

O terminal mostrará:

```text
Username
Password
```

Utilize essas credenciais para entrar no painel.

> Não publique prints que mostrem o usuário, a senha ou outras credenciais.

---

## 16. Alterar a senha do administrador

Depois do primeiro login, será exibida a tela **Panel Config**.

Na linha do usuário:

```text
admin
```

clique no ícone de cadeado localizado na coluna **Edit**.

![Localização do botão para alterar a senha do administrador](crafty-alterar-senha.png)

Depois:

1. Digite uma nova senha.
2. Confirme a senha.
3. Salve a alteração.

---

## 17. Testar a nova senha

Depois de salvar:

1. Clique no ícone do usuário no canto superior direito.
2. Selecione **Logout**.
3. Entre novamente utilizando:

```text
Username: admin
```

4. Digite a nova senha.
5. Clique em **Login**.

---

# Parte 3 — Criando o servidor Minecraft Fabric

## 18. Abrir o Crafty novamente

Caso o Codespace tenha sido desligado ou reiniciado, abra um terminal e execute:

```bash
/workspaces/nome-do-repositorio/Minecraft/run_crafty.sh
```

Depois:

1. Abra a aba **Portas**.
2. Clique no endereço do Crafty.
3. Entre com o usuário `admin`.
4. Digite a senha cadastrada.

---

## 19. Criar um novo servidor

No painel do Crafty, clique em:

```text
Create New Server
```

---

## 20. Configurar o servidor

Na página de criação, preencha os campos.

### Server Type

Selecione:

```text
Minecraft Servers
```

### Server Select

Selecione:

```text
Fabric
```

### Server Version

Escolha a versão do Minecraft que deseja utilizar.

Exemplo:

```text
1.21.11
```

A versão deve ser compatível com os mods que serão instalados.

### Server Name

Escolha qualquer nome para identificar o servidor.

Exemplo:

```text
Servidor Fabric
```

### Memória mínima

Recomendação inicial:

```text
2 GB
```

Caso o campo utilize megabytes:

```text
2048
```

### Memória máxima

Recomendação inicial:

```text
6 GB
```

Caso o campo utilize megabytes:

```text
6144
```

A quantidade ideal depende do número de jogadores, dos mods utilizados e da memória disponível no Codespace.

---

## 21. Construir e iniciar o servidor

Depois de revisar as configurações, clique em:

```text
Build Server
```

Aguarde o Crafty baixar e preparar os arquivos.

Quando o servidor estiver criado, clique em:

```text
Start
```

Na primeira inicialização, será necessário aceitar o EULA do Minecraft.

Quando solicitado, selecione:

```text
Yes
```

Depois, clique novamente em **Start**, caso o servidor não inicie automaticamente.

---

## 22. Verificar o `server.properties`

Dentro do servidor:

1. Abra a seção **Files**.
2. Localize:

```text
server.properties
```

3. Abra o arquivo.

Procure pela opção:

```properties
online-mode=true
```

Manter essa configuração como `true` ativa a autenticação oficial do Minecraft e impede que jogadores entrem utilizando o nome de outras pessoas.

Depois de alterar qualquer opção no `server.properties`, salve o arquivo e reinicie o servidor.

---

# Parte 4 — Configurando o Playit.gg

O Playit.gg será utilizado para criar um endereço público para o servidor sem precisar abrir portas manualmente no roteador.

## 23. Criar uma conta no Playit.gg

Acesse:

[Playit.gg](https://playit.gg/)

Crie uma conta ou faça login.

---

## 24. Criar um agente Docker

No painel do Playit.gg:

1. Abra a área de configuração de agentes.
2. Escolha a instalação utilizando **Docker**.
3. Defina um nome para o agente.

Exemplo:

```text
server
```

O Playit mostrará duas opções:

* Docker Run
* Docker Compose

Para este tutorial, utilize somente:

```text
Docker Run
```

Clique em **Copy** para copiar o comando completo.

> O comando contém uma `SECRET_KEY`. Não compartilhe essa chave, não coloque o comando real no GitHub e não publique prints mostrando a credencial.

O comando apresentado terá um formato semelhante a:

```bash
docker run --rm -it --net=host \
  -e SECRET_KEY="COLE_AQUI_SUA_SECRET_KEY" \
  ghcr.io/playit-cloud/playit-agent:0.17
```

No tutorial público, utilize apenas esse modelo. Cada usuário deverá copiar o próprio comando no painel do Playit.gg.

---

## 25. Executar o agente no Codespace

Abra um novo terminal no Codespace.

Não utilize o terminal que está executando o Crafty.

Cole o comando **Docker Run** fornecido pelo Playit.gg e pressione **Enter**.

O terminal começará a mostrar mensagens semelhantes a:

```text
tunnel running, 0 tunnels registered
```

Isso significa que o agente está online, mas ainda não possui nenhum túnel configurado.

Deixe esse terminal aberto.

---

## 26. Confirmar que o agente está conectado

Volte ao painel do Playit.gg.

O agente deverá aparecer como conectado.

Uma mensagem semelhante a esta poderá ser exibida:

```text
Connected
```

ou:

```text
Connected to NYC, New York USA
```

Isso confirma que o agente do Codespace está vinculado à sua conta.

---

## 27. Criar o túnel do Minecraft

No painel do Playit.gg:

1. Abra a aba **Tunnels**.
2. Clique em **Create Tunnel**.
3. Escolha **Minecraft Java**.
4. Selecione o agente criado anteriormente.
5. Configure o endereço local como:

```text
127.0.0.1
```

6. Configure a porta local como:

```text
25565
```

7. Salve o túnel.

Depois disso, o Playit.gg criará um endereço público para o servidor.

O endereço poderá ter um formato parecido com:

```text
nome-do-servidor.playit.gg
```

Copie o endereço gerado e envie para as pessoas que entrarão no servidor.

---

# Parte 5 — Entrando no servidor

No Minecraft Java:

1. Abra **Multiplayer**.
2. Clique em **Add Server**.
3. Escolha um nome para o servidor.
4. Cole o endereço gerado pelo Playit.gg.
5. Salve.
6. Entre no servidor.

Todos os jogadores deverão utilizar:

* a mesma versão do Minecraft;
* o Fabric Loader compatível;
* os mesmos mods exigidos pelo servidor;
* versões compatíveis dos mods.

---

# Como iniciar o servidor novamente

Quando o GitHub Codespace ficar ocioso, for desligado ou for aberto novamente, será necessário iniciar os componentes manualmente.

## 1. Iniciar o Crafty Controller

Abra um terminal e execute:

```bash
/workspaces/nome-do-repositorio/Minecraft/run_crafty.sh
```

Exemplo:

```bash
/workspaces/minecraft-fabric-server-codespaces/Minecraft/run_crafty.sh
```

Mantenha esse terminal aberto.

Depois:

1. Abra a aba **Portas**.
2. Clique no endereço do Crafty.
3. Faça login.
4. Entre no servidor criado.
5. Clique em **Start**.

---

## 2. Iniciar o Playit.gg

Abra outro terminal.

Entre no painel do Playit.gg, localize o agente e copie novamente o comando **Docker Run**.

O comando terá este formato:

```bash
docker run --rm -it --net=host \
  -e SECRET_KEY="SUA_SECRET_KEY" \
  ghcr.io/playit-cloud/playit-agent:0.17
```

Mantenha esse terminal aberto.

> Não salve a chave real no README, em scripts públicos ou em commits do GitHub.

---

## 3. Confirmar que tudo está funcionando

Antes de tentar entrar no Minecraft, confirme:

* O Crafty Controller está executando.
* O servidor está com o status online.
* O terminal do Playit.gg está aberto.
* O agente aparece conectado no painel do Playit.gg.
* O túnel Minecraft Java está ativo.
* A porta local está configurada como `25565`.

---

# Resumo dos terminais

Durante o funcionamento do servidor, mantenha dois terminais ativos.

### Terminal 1 — Crafty Controller

```bash
/workspaces/nome-do-repositorio/Minecraft/run_crafty.sh
```

### Terminal 2 — Playit.gg

```bash
docker run --rm -it --net=host \
  -e SECRET_KEY="SUA_SECRET_KEY" \
  ghcr.io/playit-cloud/playit-agent:0.17
```

O servidor de Minecraft também deverá estar iniciado dentro do painel do Crafty.

---

# Resumo dos comandos de instalação

```bash
sudo apt update && sudo apt upgrade && sudo apt install git
```

```bash
clear
```

```bash
pip install distro
```

```bash
git clone https://gitlab.com/crafty-controller/crafty-installer-4.0.git
```

```bash
cd crafty-installer-4.0
```

```bash
sudo ./install_crafty.sh
```

Depois da instalação:

```bash
/workspaces/nome-do-repositorio/Minecraft/run_crafty.sh
```

Caso seja necessário instalar o módulo `distro` no Python utilizado pelo instalador:

```bash
sudo python3 -m pip install distro --break-system-packages
```

---

# Resumo das respostas do instalador

| Pergunta                                | Resposta                                    |
| --------------------------------------- | ------------------------------------------- |
| Continuar a instalação no Ubuntu        | `Y`                                         |
| Instalar em `/var/opt/minecraft/crafty` | `N`                                         |
| Diretório de instalação                 | `/workspaces/nome-do-repositorio/Minecraft` |
| Branch do Crafty                        | `master`                                    |
| Criar arquivo de serviço                | `N`                                         |

---

# Observações importantes

* O GitHub Codespaces pode desligar o ambiente por inatividade.
* O servidor não ficará disponível quando o Codespace estiver desligado.
* Não feche os terminais do Crafty e do Playit enquanto estiver jogando.
* Nunca publique senhas ou a `SECRET_KEY` do Playit.gg.
* Não envie a pasta completa do servidor para o GitHub.
* Mundos, logs, bancos de dados e configurações privadas devem ficar fora do versionamento.
* Verifique sempre a compatibilidade entre Minecraft, Fabric Loader, Fabric API e mods.
