# Telegram Bot Tutorial
## Building a Telegram Bot with JavaScript

This guide will walk you through the process of building a Telegram bot using JavaScript and [Telegraf](https://github.com/telegraf/telegraf).

For this project, I've utilized JavaScript classes. Therefore, having a basic understanding of JavaScript and object-oriented programming (OOP) is recommended. If you're new to JavaScript, you can start learning from [W3Schools](https://www.w3schools.com/js/). Additionally, you can learn about object-oriented programming from [Wikipedia](https://en.wikipedia.org/wiki/Object-oriented_programming).

### Prerequisites

Before getting started, ensure you have the following installed:

1. [Node.js](https://github.com/nvm-sh/nvm)
2. [npm](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm) (Node.js package manager)
3. [Git](https://github.com/git-guides/install-git) (Version control system)

### Set Up Your Telegram Bot

1. Create a new bot on Telegram by chatting with @BotFather. Creating a new bot on Telegram is straightforward. You can refer to this [document](https://core.telegram.org/bots/tutorial#obtain-your-bot-token) for step-by-step guidance to easily create your Telegram bot. Note down the bot token provided by BotFather. You will need this token to authenticate your bot.
2. Clone this repository to your local machine
    ```
    git clone https://github.com/baibhavmandal/TelegramBotTutorial.git
    ```
3. Navigate to the project directory:
   ```
   cd your-repo
   ```
4. Install Telegraf, the Telegram bot framework for Node.js
   ```
   npm install telegraf
   ```
### Build Your Bot
1. Install Nodemon, a utility that monitors changes in your Node.js application and automatically restarts the server
   ```
   npm i nodemon
   ```
2. Update your package.json file to include scripts for starting the server in development mode with Nodemon
   ```
   "scripts": {
    ...
    "start": "node index.js",
    "dev": "nodemon index.js"
  }
    ```
3. Install dotenv, a module that allows you to store your bot token securely
    ```
    npm i dotenv
    ```
4. Create a .env file in your project directory and save your bot token
    ```
    BOT_TOKEN=YOUR_BOT_TOKEN
    ```
5.  Alternatively, you can skip the individual install steps. After cloning the project, simply run the following command in your terminal
    ```
    npm install
    ```
6. Now let's launch our bot. Run the following command in your terminal
    ```
    npm run dev
    ```
7. Congratulations! You have successfully built and deployed your first Telegram bot locally from your desktop.

### Code Explanation

Now, let's dive into the bot code. I've referenced the Telegram documentation while writing this code. While Telegram's tutorials are helpful for beginners, they lack JavaScript examples for those who prefer to build their bots using JavaScript. You can refer to this [documentation](https://core.telegram.org/bots/tutorial) while learning to build your first bot, and feel free to check out the JavaScript code provided here for guidance.

1. **Importing Telegraf Module**: The Telegraf module is imported along with the Markup object from the telegraf package. This package allows for easy interaction with the Telegram Bot API.
   ```
   const { Telegraf, Markup } = require("telegraf");
   ```
2. **Environment Configuration**: The dotenv module is required to load environment variables from a .env file, which typically stores sensitive data like API tokens.
   ```
   require("dotenv").config();
   ```
3. The **MyBot** class is a JavaScript class that defines a Telegram bot using the Telegraf framework.
   ```
   class MyBot {
    ...
   }
   ```
4. **Bot Initialization**: In the MyBot class constructor, the bot instance is initialized by providing the bot token. Additionally, initial states are configured, including the activation of "scream" mode if applicable. Furthermore, the constructor orchestrates the setup of keyboards and the registration of handlers through the **setupKeyboards** and **registerHandlers** methods, respectively.
   ```
   constructor(token) {
    this.bot = new Telegraf(token);
    this.isScreaming = false;
    // Set keyboard
    this.setupKeyboards();

    // Register command and message handlers
    this.registerHandlers();
  }
   ```
5. **Setup Keyboards**: The **setupKeyboards** method creates inline keyboards using the Markup object. These keyboards include buttons for navigation and external links.
   ```
   setupKeyboards() {
    this.nextButton = Markup.button.callback("Next", "next");
    this.backButton = Markup.button.callback("Back", "back");
    this.urlButton = Markup.button.url(
      "Tutorial",
      "https://core.telegram.org/bots/api"
    );
    this.keyboardM1 = Markup.inlineKeyboard([this.nextButton]);
    this.keyboardM2 = Markup.inlineKeyboard([this.backButton, this.urlButton]);
  }
  ```
6. **Register Handlers**: Command and message handlers are registered using the **bot.command** and **bot.on** methods. These handlers define how the bot responds to user commands, messages and action.
  ```
  registerHandlers() {
    // Command handlers
    this.bot.start(this.handleStart.bind(this));
    this.bot.help(this.handleHelp.bind(this));
    this.bot.command("scream", this.handleScreamCommand.bind(this));
    this.bot.command("whisper", this.handleWhisperCommand.bind(this));
    this.bot.command("menu", this.handleMenuCommand.bind(this));
    this.bot.command("image", this.handleImageCommand.bind(this));
    this.bot.command("aura", this.handleAuraCommand.bind(this));

    // Message handler
    this.bot.on("text", this.handleTextMessage.bind(this));

    // Action handler
    this.bot.action("next", this.handleNextButton.bind(this));
    this.bot.action("back", this.handleBackButton.bind(this));
  }
  ```
7. **Message Handling**: The **handleTextMessage** method echoes back the received message to the user. If the bot is in "scream" mode, it converts the message to uppercase before sending it back.
8. **Command Handlers**: Various command handlers are defined, such as **handleStart**, **handleHelp**, **handleScreamCommand**, etc. These methods execute specific actions in response to user commands.
9. **Action Handlers**: Action handlers are registered to handle button clicks on inline keyboards. For example, **handleNextButton** and **handleBackButton** switch between menu screens.
10. **Bot Launch**: Finally, the **startPolling** method launches the bot, allowing it to listen for incoming messages and events.
11. This part of the code is responsible for launching the Telegram bot.
  ```
  const botToken = process.env.BOT_TOKEN;
  const bot = new MyBot(botToken);
  bot.startPolling();
  ```
I trust this documentation serves as a helpful resource to kickstart your journey in building Telegram bots using JavaScript.

You can connect with me on [LinkedIn](https://www.linkedin.com/in/baibhavmandal/) for the latest updates on Node.js code for servers or Telegram bots.
