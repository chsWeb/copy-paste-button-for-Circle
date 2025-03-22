# Copy & Paste Say Hello Button for Circle

Everybody loves a warm welcome! This project provides a simple, customizable code snippet that lets new Circle community members easily greet each other with a pre-formatted message. With just one click, users can copy the greeting template and paste it as a new comment—no technical expertise required!

## Features

- **Easy to Use:** A single click on the "Copy Template" button copies a ready-to-use greeting message.
- **Customizable:** Update the template with your own details such as your name, location, or fun fact.
- **Designed for Everyone:** Ideal for non-technical users wanting to engage with the community.

## How It Works

When you add this snippet to your Circle post, the button becomes active. Clicking it automatically copies a formatted message template to your clipboard. You then simply paste it as a new comment and personalize it with your details.

### What’s Included

- **HTML:** Defines the structure of the button and message area.
- **CSS:** Styles the layout and appearance of the button and wrapper.
- **JavaScript:** Handles the clipboard functionality so the template is copied instantly.

## Watch a Tutorial
Watch the video tutorial below for a step-by-step guide on how to implement [this code](#code-snippet):
<a href="https://youtu.be/yodagnrm4S8" target="_blank">
  <img src="https://img.youtube.com/vi/yodagnrm4S8/maxresdefault.jpg" alt="Watch the video" style="max-width:100%;">
</a>

## Code Snippet
Copy and paste the code below into the HTML enter field in your Circle Post > Settings.

```html
<style>
  /* Padding for the wrapper */
  #idl-wrap {
    padding: 24px 0;
  }

  /* Button styling inside #idl-wrap */
  #idl-wrap #btn {
    background: #080808;
    color: #f5f5f5;
    padding: 4px 12px;
    cursor: pointer;
    border-radius: 6px;
    margin-top: 16px;
  }
</style>

<div id="idl-wrap">
  <button id="btn">Copy Template</button>
  <p id="msg" style="display: none; color: green;">
    Copied! Paste as a new comment below.
  </p>
</div>

<script>
  document.getElementById('btn').addEventListener('click', function () {
    const raw = `👋 **Your Name**:\u200B
📍 **Location**:\u200B
🎯 **My Favorite Animal is**:\u200B
💡 **A fun fact about me**:\u200B`;

    const template = raw
      .split('\n')
      .map(line => line.trim())
      .join('\n');

    navigator.clipboard.writeText(template).then(() => {
      const msg = document.getElementById('msg');
      msg.style.display = 'inline';
      setTimeout(() => {
        msg.style.display = 'none';
      }, 4000);
    });
  });
</script>
```
## Have an Idea?

Contributions, suggestions, and improvements are welcome! Feel free to open an issue or submit a pull request.
