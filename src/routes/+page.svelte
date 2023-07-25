<script lang="ts">
  import axios from "axios";
  const webhookUrl =
    "https://discord.com/api/webhooks/1130183711330160660/wFu1ql_8F1cNdcM-Pov-PXT2M_ZWu1ptuGtMvBJV0K6TptkBOl-9CHMapSxZki6gyyTk";

  let message: string;
  let title: string;
  let description: string;
  let username: string;
  let url: string;
  let hexColor: string;
  let footer: { text?: string; icon_url?: string } = {};
  let form: HTMLFormElement;

  const submit = async () => {
    console.log("Sending");
    let obj: {
      content?: string;
      username?: string;
      embeds?: object[];
    } = {};

    hexColor = hexColor?.replace("#", "");
    const color = parseInt(hexColor, 16);

    if (message) obj.content = message;
    if (username) obj.username = username;
    if (title || description || url || hexColor || footer.text)
      obj.embeds = [{ title, description, url, color, footer }];

    // console.log(obj); // For Development

    try {
      await axios.post(webhookUrl, obj);
      console.log("Message sent to Discord webhook");
    } catch (error) {
      console.error("Error sending message to Discord webhook:", error);
    }

    // Value resets

    form.reset();
  };
</script>

<h1>Webhook sender</h1>
<form on:submit={submit} bind:this={form}>
  <label>
    <h2>Message</h2>
    <input type="text" bind:value={message} />
  </label>
  <label>
    <h2>Username</h2>
    <input type="text" bind:value={username} />
  </label>
  <h1>Embed</h1>
  <label>
    <h2>Title</h2>
    <input type="text" bind:value={title} />
  </label>
  <label>
    <h2>Description</h2>
    <input type="text" bind:value={description} />
  </label>
  <label>
    <h2>Url</h2>
    <input type="text" bind:value={url} />
  </label>
  <label>
    <h2>Color</h2>
    <input type="text" bind:value={hexColor} />
  </label>
  <label>
    <h2>Footer</h2>
    <input type="text" bind:value={footer.text} />
  </label>
  <button type="submit">Click</button>
</form>
