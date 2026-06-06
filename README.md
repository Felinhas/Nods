import {
  Client,
  GatewayIntentBits,
  Events,
  REST,
  Routes,
  MessageFlags,
  EmbedBuilder,
  ActionRowBuilder,
  ButtonBuilder,
  ButtonStyle,
} from "discord.js";

const token = "n";
const clientId = "";

if (!token || !clientId) {
  console.error("Missing DISCORD_TOKEN or DISCORD_CLIENT_ID environment variables.");
  process.exit(1);
}

const client = new Client({ intents: [GatewayIntentBits.Guilds] });

client.once(Events.ClientReady, async (readyClient) => {
  console.log(`[ready] Bot is online as ${readyClient.user.tag}`);
  try {
    const rest = new REST({ version: "10" }).setToken(token);
    const commands = await rest.get(Routes.applicationCommands(clientId));
    const names = commands.map((c) => `/${c.name}`).join(", ");
    console.log(`[commands] Registered global commands: ${names || "(none)"}`);
  } catch (err) {
    console.error("[commands] Failed to verify registered commands:", err.message);
  }
});

const sleep = (ms) => new Promise((resolve) => setTimeout(resolve, ms));

const SPAM_MESSAGE    = "# E O كواي E O KAZ1M MOLESTADORES DA NET TAMO ONNN";
const ULTRASPAM_MESSAGE = `
# E O KAZ1M E O كواي  PASSANDO NA SUA TELINHA lol seus filha da puta @everyone
# E O KAZ1M E O كواي  PASSANDO NA SUA TELINHA lol seus filha da puta @everyone
# E O KAZ1M E O كواي  PASSANDO NA SUA TELINHA lol seus filha da puta @everyone
# E O KAZ1M E O كواي  PASSANDO NA SUA TELINHA lol seus filha da puta @everyone
# E O KAZ1M E O كواي  PASSANDO NA SUA TELINHA lol seus filha da puta @everyone
# E O KAZ1M E O كواي  PASSANDO NA SUA TELINHA lol seus filha da puta @everyone
# E O KAZ1M E O كواي  PASSANDO NA SUA TELINHA lol seus filha da puta @everyone
# E O KAZ1M E O كواي  PASSANDO NA SUA TELINHA lol seus filha da puta @everyone
# E O KAZ1M E O كواي  PASSANDO NA SUA TELINHA lol seus filha da puta @everyone
# E O KAZ1M E O كواي  PASSANDO NA SUA TELINHA lol seus filha da puta @everyone
# E O KAZ1M E O كواي  PASSANDO NA SUA TELINHA lol seus filha da puta @everyone
# E O KAZ1M E O كواي  PASSANDO NA SUA TELINHA lol seus filha da puta @everyone
# E O KAZ1M E O كواي  PASSANDO NA SUA TELINHA lol seus filha da puta @everyone
# E O KAZ1M E O كواي  PASSANDO NA SUA TELINHA lol seus filha da puta @everyone
# E O KAZ1M E O كواي  PASSANDO NA SUA TELINHA lol seus filha da puta @everyone
# E O KAZ1M E O كواي  PASSANDO NA SUA TELINHA lol seus filha da puta @everyone
# E O KAZ1M E O كواي  PASSANDO NA SUA TELINHA lol seus filha da puta @everyone
# E O KAZ1M E O كواي  PASSANDO NA SUA TELINHA lol seus filha da puta @everyone
# E O KAZ1M E O كواي  PASSANDO NA SUA TELINHA lol seus filha da puta @everyone
# E O KAZ1M E O كواي  PASSANDO NA SUA TELINHA lol seus filha da puta @everyone
# E O KAZ1M E O كواي  PASSANDO NA SUA TELINHA lol seus filha da puta @everyone
# E O KAZ1M E O كواي  PASSANDO NA SUA TELINHA lol seus filha da puta @everyone
	# E O KAZ1M E O كواي  PASSANDO NA SUA TELINHA lol seus filha da puta @everyone
# E O KAZ1M E O كواي  PASSANDO NA SUA TELINHA lol seus filha da puta @everyone
`;
const PANEL_SPAM_MESSAGE = "# E O KAZ1M E O كواي PASSANDO NA SUA TELINHA lol seus filha da puta";

client.on(Events.InteractionCreate, async (interaction) => {

  // ── Button handler ──────────────────────────────────────────────────────────
  if (interaction.isButton()) {
    if (interaction.customId === "panel_spam") {
      try {
        await interaction.reply({ content: "Enviando", flags: MessageFlags.Ephemeral });
        for (let i = 0; i < 15; i++) {
          await interaction.followUp({ content: PANEL_SPAM_MESSAGE });
          if (i < 14) await sleep(100);
        }
      } catch (error) {
        console.error("[panel_spam] Error:", error.message);
      }
    }
    return;
  }

  if (!interaction.isChatInputCommand()) return;

  // ── /panel ──────────────────────────────────────────────────────────────────
  if (interaction.commandName === "panel") {
    try {
      const embed = new EmbedBuilder().setTitle("Spam").setColor(0xff0000);
      const row = new ActionRowBuilder().addComponents(
        new ButtonBuilder()
          .setCustomId("panel_spam")
          .setLabel("CLICK")
          .setStyle(ButtonStyle.Danger)
      );
      await interaction.reply({ embeds: [embed], components: [row], flags: MessageFlags.Ephemeral });
    } catch (error) {
      console.error("[panel] Error:", error.message);
      if (!interaction.replied && !interaction.deferred)
        await interaction.reply({ content: "Something went wrong.", flags: MessageFlags.Ephemeral });
    }
  }

  // ── /ultraspam ───────────────────────────────────────────────────────────────
  if (interaction.commandName === "ultraspam") {
    try {
      await interaction.reply({ content: "Enviando", flags: MessageFlags.Ephemeral });
      for (let i = 0; i < 15; i++) {
        await interaction.followUp({ content: ULTRASPAM_MESSAGE });
        if (i < 14) await sleep(100);
      }
    } catch (error) {
      console.error("[ultraspam] Error:", error.message);
      if (!interaction.replied && !interaction.deferred)
        await interaction.reply({ content: "Something went wrong.", flags: MessageFlags.Ephemeral });
    }
  }

  // ── /spam ────────────────────────────────────────────────────────────────────
  if (interaction.commandName === "spam") {
    const customText = interaction.options.getString("text");
    const message = customText ?? SPAM_MESSAGE;
    try {
      await interaction.reply({ content: "Enviando", flags: MessageFlags.Ephemeral });
      for (let i = 0; i < 15; i++) {
        await interaction.followUp({ content: message });
        if (i < 14) await sleep(200);
      }
    } catch (error) {
      console.error("[spam] Error:", error.message);
      if (!interaction.replied && !interaction.deferred)
        await interaction.reply({ content: "Something went wrong.", flags: MessageFlags.Ephemeral });
    }
  }

  // ── /mg ──────────────────────────────────────────────────────────────────────
  if (interaction.commandName === "mg") {
    const text = interaction.options.getString("text");
    try {
      await interaction.reply({ content: "Enviando", flags: MessageFlags.Ephemeral });
      await interaction.followUp({ content: text });
    } catch (error) {
      console.error("[mg] Error:", error.message);
      if (!interaction.replied && !interaction.deferred)
        await interaction.reply({ content: "Something went wrong.", flags: MessageFlags.Ephemeral });
    }
  }
});

client.on(Events.Error, (e) => console.error("[error]", e.message));
client.on(Events.Warn, (m) => console.warn("[warn]", m));
client.on(Events.ShardDisconnect, (e, id) => console.warn(`[disconnect] Shard ${id} disconnected (code ${e.code})`));
client.on(Events.ShardReconnecting, (id) => console.log(`[reconnect] Shard ${id} reconnecting...`));
client.on(Events.ShardResume, (id, n) => console.log(`[resume] Shard ${id} resumed (${n} events replayed)`));

process.on("unhandledRejection", (r) => console.error("[unhandledRejection]", r));
process.on("uncaughtException", (e) => console.error("[uncaughtException]", e.message));

client.login(token);
