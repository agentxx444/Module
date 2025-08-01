# Module
Chatbot Widget Module

Copy all code and paste it in your smm site. How?
Go to your admin side, appearance > theme > actions > edit theme > and then find the script.js and paste the code then save. Done! Easy!

COPY ALL CODE BELOW
```html
/* 
ChatBot Widget
*/

(function () {
  const chatContainer = document.createElement('div');
  chatContainer.style.position = 'fixed';
  chatContainer.style.bottom = '20px';
  chatContainer.style.right = '20px';
  chatContainer.style.width = '320px';
  chatContainer.style.height = '40px'; // Start minimized
  chatContainer.style.border = '1px solid #ccc';
  chatContainer.style.background = '#fff';
  chatContainer.style.boxShadow = '0 0 10px rgba(0,0,0,0.2)';
  chatContainer.style.zIndex = '10000';
  chatContainer.style.borderRadius = '10px';
  chatContainer.style.overflow = 'hidden';
  chatContainer.style.transition = 'height 0.3s ease';

  const header = document.createElement('div');
  header.style.height = '40px';
  header.style.background = '#4a90e2';
  header.style.color = '#fff';
  header.style.display = 'flex';
  header.style.alignItems = 'center';
  header.style.justifyContent = 'space-between';
  header.style.padding = '0 10px';
  header.style.fontSize = '14px';
  header.style.fontWeight = 'bold';
  header.style.cursor = 'pointer';

  header.textContent = '💬 TrendspherePro AI Assistant';

  const toggleBtn = document.createElement('button');
  toggleBtn.textContent = '+'; // Expand icon
  toggleBtn.style.background = 'transparent';
  toggleBtn.style.border = 'none';
  toggleBtn.style.color = '#fff';
  toggleBtn.style.cursor = 'pointer';
  toggleBtn.style.fontSize = '18px';
  toggleBtn.style.marginLeft = 'auto';

  header.appendChild(toggleBtn);
  chatContainer.appendChild(header);

  const iframe = document.createElement('iframe');
  iframe.src = "https://smmprov.com/chat-widget?site=" + encodeURIComponent(window.location.origin);
  iframe.style.width = '100%';
  iframe.style.height = 'calc(100% - 40px)';
  iframe.style.border = 'none';
  iframe.style.display = 'none'; // Hidden initially

  chatContainer.appendChild(iframe);
  document.body.appendChild(chatContainer);

  let minimized = true;
  let welcomeShown = false;

  iframe.addEventListener('load', () => {
    header.onclick = () => {
      minimized = !minimized;
      iframe.style.display = minimized ? 'none' : 'block';
      chatContainer.style.height = minimized ? '40px' : '440px';
      toggleBtn.textContent = minimized ? '+' : '–';

      if (!minimized && !welcomeShown) {
        iframe.contentWindow.postMessage({
          type: 'showWelcomeMessage',
          message: `Ask Me Anything!

ℹ️ Now you can use the bot features:

🧪 Type: service <service_id>
To check if a service is fast, normal, or slow.
Ex: service 5152

🎯 Type: suggest <keyword>
To get service suggestions related to your keyword.
Ex: suggest facebook followers

🚧 Note: This feature is in beta and may change anytime.`
        }, '*');
        welcomeShown = true;
      }
    };
  });
})();

