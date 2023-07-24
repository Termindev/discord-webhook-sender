<script lang="ts">
  import axios from "axios";
  const webhookUrl = "WEBHOOKURL";
  let message: string | undefined;
  let title: string | undefined;
  let description: string | undefined;
  let username: string | undefined;
  let url: string | undefined;
  let color: string | undefined;
  let footer: { text?: string; icon_url?: string } = {};
  let imageInput: HTMLInputElement;

  const submit = async () => {
    console.log("Sending");
    let obj: {
      content?: string;
      username?: string;
      embeds?: object[];
    } = {};

    const formData = new FormData();
    formData.append("image", imageInput.files[0]);

    if (message) obj.content = message;
    if (username) obj.username = username;
    if (title || description || url || color || footer.text)
      obj.embeds = [{ title, description, url, color, footer }];
    console.log(obj);
    try {
      const response = await axios.post(webhookUrl, obj);
      console.log("Message sent to Discord webhook");
    } catch (error) {
      console.error("Error sending message to Discord webhook:", error);
    }
    message = undefined;
    title = undefined;
    description = undefined;
    url = undefined;
    color = undefined;
  };
</script>

<h1>Webhook sender</h1>
<form on:submit={submit}>
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
    <input type="text" bind:value={color} />
  </label>
  <label>
    <h2>Footer</h2>
    <input type="text" bind:value={footer.text} />
  </label>
  <label>
    <h2>Footer image</h2>
    <input type="file" bind:this={imageInput} name="image" />
  </label>
  <button type="submit">Click</button>
</form>
