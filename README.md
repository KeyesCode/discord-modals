<div align="center">
  <img src="https://cdn.discordapp.com/attachments/910547379617402960/942871547268436088/Discord-Modals.png" alt="Discord Modals" />
  <p align="center">
  <a href="https://www.npmjs.com/package/discord-modals">
    <img src="https://img.shields.io/npm/dt/discord-modals?style=for-the-badge" alt="npm" />
  </a>

  <a href="https://discord.gg/dscbots">
    <img src="https://img.shields.io/discord/852531635252494346?color=5865F2&label=Discord Server&style=for-the-badge" alt="Discord Server" />
  </a>
</p>

</div>

> **A package that allows your bot of discord.js v13 to create the new Discord Modals and interact with them.**

# 🔎 Installation

```sh
npm install discord-modals
```

# 🔮 What is this package for?

Recently, Discord announced Modal Interactions. What is that? Modal is a popup of Text Input Components [[Example]](https://media.discordapp.net/attachments/910547379617402960/942881133379612682/Modals_Test.png?width=881&height=559). It's so cool. However, discord.js hasn't added it yet. discord-modals can be a solution if you want to test or use modals right now in v13. Try it!

# ✨ Setup

```js
const { Client } = require('discord.js') // Extract the Client class
const client = new Client({ intents: 32767 }) // Create a Client
const discordModals = require('discord-modals') // Define the discord-modals package!
discordModals(client); // discord-modals needs your client in order to interact with modals

client.login('token') // Login with your bot
```

# ❓ How can i use it?

> First of all, we need to understand that Modals and Text Input Components are completely different. Modals is a popup that shows the text input components and text input are the components of modals. To understand better, you can explore the Discord API Documentation [here](https://discord.com/developers/docs/interactions/message-components#text-inputs).

**Modals have:**
- A Title.
- A Custom Id.
- Components (Text Input)

**Text Input have:**
- A Custom Id
- A Style (Short or Paragraph)
- A Label
- A minimum length
- A maximum length
- A value (A prefilled value if there is not text)
- And...a place holder

If you have understood this, you can continue on "Examples" section.

# 📜 Examples

If you are ready, take this examples.

- First, we are going to create a Modal.

```js
const { Modal } = require('discord-modals') // Modal class

const modal = new Modal() // We create a Modal
.setCustomId('customid')
.setTitle('Test of Discord-Modals!')
.addComponents()
```
> **This is a basic structure of a Modal, but something is missing. Yeah! Text Input components.**

- We are going to create and add a Text Input Component to the Modal.

```js
const { Modal, TextInputComponent } = require('discord-modals') // Modal & TextInputComponent class

const modal = new Modal() // We create a Modal
.setCustomId('customid')
.setTitle('Test of Discord-Modals!')
.addComponents(
  new TextInputComponent() // We create an Text Input Component
  .setCustomId('customid')
  .setLabel('Some text Here')
  .setStyle('SHORT') //IMPORTANT: Text Input Component Style can be 'SHORT' or 'LONG'
  .setMinLength(4)
  .setMaxLength(10)
  .setPlaceholder('Write a text here')
  .setRequired(true) // If it's required or not
  .setValue('value')  
);
```

> **Yay! We have the full Modal & Text Input Component, but... How can i send a Modal?** 

- We are going to use the `showModal()` method to send the modal in an interaction.

```js
const { Modal, TextInputComponent, showModal } = require('discord-modals') // Now we extract the showModal method

const modal = new Modal() // We create a Modal
.setCustomId('customid')
.setTitle('Test of Discord-Modals!')
.addComponents(
  new TextInputComponent() // We create an Text Input Component
  .setCustomId('customid')
  .setLabel('Some text Here')
  .setStyle('SHORT') //IMPORTANT: Text Input Component Style can be 'SHORT' or 'LONG'
  .setMinLength(4)
  .setMaxLength(10)
  .setPlaceholder('Write a text here')
  .setRequired(true) // If it's required or not
  .setValue('value')  
);

client.on('interactionCreate', (interaction) => {
  // Let's say that the interaction will be an Slash Command called 'ping'.
  if(interaction.commandName === 'ping'){
    showModal(modal, {
      client: client, // The showModal() method needs the client to send the modal through the API.
      interaction: interaction // The showModal() method needs the interaction to send the modal with the Interaction ID & Token.
    })
  }
  
})

```

> **Congrats! You show the Modal to the Interaction User. Now, how can i receive the modal interaction?**

- discord-modals integrates a new event to your Client called `modalSubmit`. We are going to use it.
- To have access to the responses, just use the `.components` property (Array) and then, use the `.value` property.

```js
client.on('modalSubmit', (modal) => {
  if(modal.customId === 'customid'){
    const firstResponse = modal.components[0].value
    modal.reply('Congrats! Powered by discord-modals.' + `\`\`\`${firstResponse}\`\`\``)
  }  
})
```

> **And you made it! I hope this examples help you :)**

![Final Result](https://cdn.discordapp.com/attachments/910547379617402960/943208236478247032/Discord-Modals-Test.gif)

# 📚 Documentation
- Check our documentation [here](https://github.com/Mateo-tem/discord-modals/blob/master/DOCS.md).

# 🔨 Developers
- 『𝑴𝒂𝒕𝒆𝒐ᵗᵉᵐ』#9999

# ⛔ Issues/Bugs?
> **Please report it on our GitHub Repository [here](https://github.com/Mateo-tem/discord-modals/issues) to fix it inmmediately.**