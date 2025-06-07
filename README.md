# 🤖 Naylor Discord

Este projeto é uma estrutura base para criar um bot do Discord utilizando a biblioteca `discord.js`, com um sistema modular para carregar comandos e eventos de forma organizada.

---

## ✨ Funcionalidades

* **Sistema de Comandos Modular**: Carrega comandos dinamicamente de pastas, permitindo organizar suas funcionalidades em categorias.
* **Sistema de Eventos Modular**: Carrega eventos do Discord (como `ready`, `interactionCreate`) de arquivos separados, mantendo o código limpo e organizado.
* **Configuração Fácil**: Utiliza um arquivo `config.json` para armazenar o token do bot.

---

## ⚙️ Pré-requisitos

Certifique-se de ter o seguinte instalado em sua máquina:

* **Node.js**: Versão 16.x ou superior.
* **npm** ou **Yarn**: Gerenciador de pacotes.

---

## 📦 Instalação

Siga os passos abaixo para colocar o projeto em funcionamento:

1.  **Clone o repositório** (ou copie o código para um novo arquivo `index.js`):

    ```bash
    git clone <url_do_seu_repositorio>
    cd <nome_da_pasta>
    ```

    Se você copiou o código, crie um arquivo chamado `index.js` e cole o conteúdo fornecido.

2.  **Instale as dependências**:

    ```bash
    npm install discord.js
    # ou
    yarn add discord.js
    ```

3.  **Crie o arquivo de configuração**:

    Na raiz do projeto, crie um arquivo chamado `config.json` e adicione o token do seu bot:

    ```json
    {
        "token": "SEU_TOKEN_DO_BOT_AQUI"
    }
    ```

    Você pode obter o token do seu bot na página do [Discord Developer Portal](https://discord.com/developers/applications).

---

## 🚀 Como Usar

### 1. Estrutura de Pastas

O bot espera que seus **comandos** e **eventos** estejam organizados em pastas específicas na raiz do projeto:

* `Commands/`: Contém subpastas para organizar seus comandos por categoria.
* `Events/`: Contém os arquivos dos seus eventos.

A estrutura deve ser similar a esta:

```
.
├── index.js
├── config.json
├── Commands/
│   ├── Categoria1/
│   │   └── meucomando.js
│   └── Categoria2/
│       └── outrocomando.js
└── Events/
    ├── ready.js
    └── interactionCreate.js
```

### 2. Criando um Comando

Cada arquivo de comando (`.js`) dentro de `Commands/` deve exportar um objeto com as propriedades `data` e `execute`.

* `data`: Um objeto `SlashCommandBuilder` do `discord.js` que define o comando (nome, descrição, opções, etc.).
* `execute`: Uma função assíncrona que será executada quando o comando for chamado. Ela recebe o objeto `interaction` do Discord.

**Exemplo de comando (`Commands/Util/ping.js`):**

```javascript
const { SlashCommandBuilder } = require('discord.js');

module.exports = {
    data: new SlashCommandBuilder()
        .setName('ping')
        .setDescription('Responde com Pong!'),
    async execute(interaction) {
        await interaction.reply('Pong!');
    },
};
```

### 3. Criando um Evento

Cada arquivo de evento (`.js`) dentro de `Events/` deve exportar um objeto com as propriedades `name`, `once` (opcional) e `execute`.

* `name`: O nome do evento do Discord que você deseja ouvir (ex: `ready`, `interactionCreate`).
* `once`: Um booleano opcional. Se `true`, o evento será executado apenas uma vez. O padrão é `false`.
* `execute`: Uma função assíncrona que será executada quando o evento ocorrer. Ela recebe os argumentos correspondentes ao evento.

**Exemplo de evento (`Events/ready.js`):**

```javascript
const { Events } = require('discord.js');

module.exports = {
    name: Events.ClientReady,
    once: true, // Este evento será executado apenas uma vez quando o bot estiver pronto
    execute(client) {
        console.log(`Pronto! Logado como ${client.user.tag}`);
    },
};
```

### 4. Rodando o Bot

Para iniciar o bot, execute o seguinte comando no terminal na raiz do projeto:

```bash
node index.js
```

---

## 🚨 Resolução de Problemas

* **`[WARNING] The command at ... is missing a required "data" or "execute" property.`**: Verifique se seus arquivos de comando (`.js`) exportam um objeto com as propriedades `data` (um `SlashCommandBuilder`) e `execute` (a função do comando).
* **`Token not found` ou erro de autenticação**: Certifique-se de que o arquivo `config.json` existe na raiz do projeto e que o `token` está correto.
* **Comandos não aparecem no Discord**: Após adicionar novos comandos ou modificar existentes, você precisará registrá-los com o Discord. Este template não inclui um script de deploy de comandos, mas você pode encontrar exemplos na documentação do `discord.js`.

---

## ❓ Precisa de ajuda?

Se tiver dúvidas ou encontrar problemas, sinta-se à vontade para revisar a documentação oficial do `discord.js` ou procurar por tutoriais e comunidades online.
