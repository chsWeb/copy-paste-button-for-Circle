# Copy & Paste Say Hello Button for Circle

Everybody loves a warm welcome! This project provides a simple, customizable code snippet that lets new Circle community members easily greet each other with a pre-formatted message. With just one click, users can copy the greeting template and paste it as a new comment—no technical expertise required!

## Features

- **Easy to Use:** A single click copies a ready-to-use greeting message to the clipboard.
- **Customizable:** Update the template with your own details and questions.
- **Designed for Everyone:** Ideal for non-technical users wanting to engage with the community.

## How It Works

When you add this snippet to the HTML section in your Circle post settings, the button becomes active. Clicking it automatically copies a formatted message template to your clipboard. You then simply paste it as a new comment and personalize it with your details.

### What’s Included

- **HTML:** Defines the structure of the button and message area.
- **CSS:** Styles the layout and appearance of the button.
- **JavaScript:** Handles the clipboard functionality so the template is copied instantly.

## Watch a Tutorial
Watch the video tutorial below for a step-by-step guide on how to implement [this code](#code-snippet):
<a href="https://youtu.be/yodagnrm4S8" target="_blank">
  <img src="https://img.youtube.com/vi/yodagnrm4S8/maxresdefault.jpg" alt="Watch the video" style="max-width:100%;">
</a>

## Code Snippet
Copy and paste the code below into the HTML enter field in your Circle Post > Settings.
- **IMPORTANT:** If you use apostrophes in your formatted message, you must put a \ before the apostrophe (‘), e.g., What\’s Your Name?

```html
<style>
  .idl-wrap {
    padding: 24px 0;
  }
  /* Desktop button styles */
  .idl-wrap .btn {
    background: #080808;
    color: #f5f5f5;
    padding: 4px 12px;
    cursor: pointer;
    border-radius: 6px;
    margin-top: 16px;
    line-height: 1em;
  }
  
  /* Touch device button styles */
  @media (hover: none) and (pointer: coarse) {
    .idl-wrap .btn {
      padding: 12px 20px;
      font-size: 1.2em;
      border-radius: 8px;
    }
  }
</style>

<div class="idl-wrap">
  <button class="btn">Copy Template</button>
  <p class="msg" style="display: none; color: green;">Copied! Paste as a new comment below.</p>
</div>

<script>
  // Define your template fields in one place.
  const fields = [
    { icon: "👋", label: "Your Name:" },
    { icon: "📍", label: "Location:" },
    { icon: "🎯", label: "What's My Favorite Color:" },
    { icon: "💡", label: "A fun fact about me:" }
  ];
  // ** DO NOT EDIT ANYTHING BELOW THIS LINE **
  // Generate the rich HTML version for desktop.
  // Each field is output as a single paragraph (<p>) with:
  // - the icon,
  // - the label in bold (<strong>), and then
  // - a non‑breaking space and a zero‑width space (&nbsp;&#8203;) outside the <strong> tag.
  const richTemplate = fields.map(field =>
    `<p>${field.icon} <strong>${field.label}</strong>&nbsp;&#8203;</p>`
  ).join('\n');

  // Generate the plain text version for mobile.
  // Each field is a single line.
  const plainTemplate = fields.map(field =>
    `${field.icon} ${field.label}`
  ).join('\n');

  // Utility: Detect mobile devices.
  function isMobileDevice() {
    return /Mobi|Android/i.test(navigator.userAgent);
  }

  // Fallback function using a hidden textarea.
  function fallbackCopyText(text) {
    const textArea = document.createElement('textarea');
    textArea.value = text;
    textArea.style.position = 'fixed';
    textArea.style.top = '0';
    textArea.style.left = '-9999px';
    document.body.appendChild(textArea);
    textArea.focus();
    textArea.select();
    let successful = false;
    try {
      successful = document.execCommand('copy');
    } catch (err) {
      console.error('Fallback copy failed:', err);
    }
    document.body.removeChild(textArea);
    return successful;
  }

  function copyTemplate(msg) {
    // Helper to show the confirmation message.
    function showMsg(msgElem) {
      msgElem.style.display = 'inline';
      setTimeout(() => { msgElem.style.display = 'none'; }, 4000);
    }

    // Use plain text on mobile; use rich HTML on desktop.
    if (isMobileDevice()) {
      if (navigator.clipboard && navigator.clipboard.writeText) {
        navigator.clipboard.writeText(plainTemplate)
          .then(() => showMsg(msg))
          .catch(err => {
            console.error('Clipboard.writeText failed:', err);
            if (fallbackCopyText(plainTemplate)) showMsg(msg);
          });
      } else {
        if (fallbackCopyText(plainTemplate)) showMsg(msg);
      }
    } else {
      // Desktop: Try using Clipboard API with HTML support.
      if (navigator.clipboard && navigator.clipboard.write) {
        const blobHtml = new Blob([richTemplate], { type: 'text/html' });
        const blobPlain = new Blob([plainTemplate], { type: 'text/plain' });
        const data = new ClipboardItem({
          'text/html': blobHtml,
          'text/plain': blobPlain
        });
        navigator.clipboard.write([data])
          .then(() => showMsg(msg))
          .catch(err => {
            console.error('Clipboard.write failed:', err);
            // Fallback to plain text.
            if (navigator.clipboard && navigator.clipboard.writeText) {
              navigator.clipboard.writeText(plainTemplate)
                .then(() => showMsg(msg))
                .catch(err => {
                  console.error('Clipboard.writeText failed:', err);
                  if (fallbackCopyText(plainTemplate)) showMsg(msg);
                });
            } else {
              if (fallbackCopyText(plainTemplate)) showMsg(msg);
            }
          });
      } else if (navigator.clipboard && navigator.clipboard.writeText) {
        navigator.clipboard.writeText(plainTemplate)
          .then(() => showMsg(msg))
          .catch(err => {
            if (fallbackCopyText(plainTemplate)) showMsg(msg);
          });
      } else {
        if (fallbackCopyText(plainTemplate)) showMsg(msg);
      }
    }
  }

  // Attach event listeners for each instance.
  document.querySelectorAll('.idl-wrap').forEach(container => {
    const btn = container.querySelector('.btn');
    const msg = container.querySelector('.msg');

    let touchTriggered = false;
    btn.addEventListener('touchend', function(e) {
      e.preventDefault();
      touchTriggered = true;
      copyTemplate(msg);
    });
    btn.addEventListener('click', function(e) {
      if (touchTriggered) {
        touchTriggered = false;
        return;
      }
      copyTemplate(msg);
    });
  });
</script>
```
## Have an Idea?

Contributions, suggestions, and improvements are welcome! Feel free to open an issue or submit a pull request.
