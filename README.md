# quiet-discordjs

quiet-discordjs is a silent, modified version of [discord.js](https://discordjs.org). It disables all internal error throwing and console logging, making it suitable for environments where stability and silence are preferred.

## Changes

- **No Errors:** Suppresses all thrown errors, including DiscordjsError, TypeError, and rejections.
- **No Logs:** Disables all console outputs such as console.log, console.error, and process warnings.

## About

quiet-discordjs (a fork of discord.js) is a powerful Node.js module that allows you to easily interact with the [Discord API](https://discord.com/developers/docs/intro).

- Object-oriented
- Predictable abstractions
- High performance
- Full coverage of the Discord API

## Installation

Node.js 18 or newer is required.

```sh
npm install quiet-discordjs
````

or

```sh
yarn add quiet-discordjs
```

### Optional packages

These packages are not part of this module, but they are supported by the underlying discord.js library.

* [zlib-sync](https://www.npmjs.com/package/zlib-sync) for WebSocket data compression
* [bufferutil](https://www.npmjs.com/package/bufferutil) for faster WebSocket performance
* [@discordjs/voice](https://www.npmjs.com/package/@discordjs/voice) for voice support

## Example usage

Registering a slash command:

```js
import djs from 'quiet-discordjs';

const commands = [
  {
    name: 'ping',
    description: 'Replies with Pong!',
  },
];

const rest = new djs.REST({ version: '10' }).setToken(TOKEN);

try {
  await rest.put(djs.Routes.applicationCommands(CLIENT_ID), { body: commands });
} catch (error) {
  return;
}
```

Creating a simple bot:

```js
import djs from 'quiet-discordjs';

const client = new djs.Client({ intents: [djs.GatewayIntentBits.Guilds] });

client.on('ready', () => {
  console.log(`Logged in as ${client.user.tag}`);
});

client.on('interactionCreate', async interaction => {
  if (!interaction.isChatInputCommand()) return;

  if (interaction.commandName === 'ping') {
    await interaction.reply('Pong!');
  }
});

client.login(TOKEN);
```

### To Block Closing When Error
```javascript
import djs from 'quiet-discordjs';

const client = new djs.Client({ intents: [djs.GatewayIntentBits.Guilds] });

client.on('ready', () => {
  console.log(`Logged in as ${client.user.tag}`);
});

client.on('messageCreate', async message => {
  if(message.author.bot) return;
  if(message.content == "a!reply") {
     try {
     message.reply(); //gonna give error, so we gonna add try
     } catch(error) {
          console.log("error") //or: return;
     }
  }
});

client.login(TOKEN);
```

## Links

These belong to the original discord.js project.

* [Website](https://discord.js.org)
* [Documentation](https://discord.js.org/docs/packages/discord.js/stable)
* [Guide](https://discordjs.guide/)
* [GitHub Repository](https://github.com/discordjs/discord.js/tree/main/packages/discord.js)
* [npm Package](https://www.npmjs.com/package/discord.js)

## Contributing

This is not an official fork. Please refer to the original [discord.js contribution guide](https://github.com/discordjs/discord.js/blob/main/.github/CONTRIBUTING.md) for details.

## Help

For help with the Discord API or discord.js behavior, please visit the [discord.js Discord server](https://discord.gg/djs).

**Note:** This library is not affiliated with or endorsed by the original discord.js team.
