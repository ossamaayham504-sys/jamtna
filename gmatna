<!DOCTYPE html>
<html lang="ar">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>شات جمعتنا للهاتف</title>
  <style>
    body {
      font-family: Arial, sans‑serif;
      background: #e0e7ff;
      margin: 0;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
    }
    .chat-container {
      width: 95%;
      max-width: 480px;
      height: 90vh;
      background: white;
      border-radius: 20px;
      display: flex;
      flex-direction: column;
      box-shadow: 0 6px 20px rgba(0,0,0,0.15);
      overflow: hidden;
    }
    header {
      padding: 12px;
      border-bottom: 1px solid #ddd;
      display: flex;
      justify-content: space-between;
      align-items: center;
      background: linear-gradient(90deg, #6366f1, #a78bfa);
      color: white;
      font-weight: bold;
      font-size: 18px;
    }
    main {
      flex: 1;
      padding: 12px;
      overflow-y: auto;
      display: flex;
      flex-direction: column;
      gap: 10px;
      background: #f3f4f6;
    }
    footer {
      display: flex;
      padding: 10px;
      border-top: 1px solid #ddd;
      gap: 8px;
      background: white;
    }
    textarea {
      flex: 1;
      resize: none;
      padding: 10px;
      border-radius: 15px;
      border: 1px solid #ccc;
      font-size: 16px;
    }
    button {
      background: #6366f1;
      color: white;
      border: none;
      border-radius: 15px;
      padding: 0 18px;
      font-size: 16px;
      cursor: pointer;
      min-width: 70px;
    }
    .message {
      max-width: 75%;
      padding: 10px 14px;
      border-radius: 20px;
      display: inline-block;
      word-wrap: break-word;
      font-size: 15px;
      line-height: 1.3;
    }
    .me {
      background: linear-gradient(90deg, #4f46e5, #a78bfa);
      color: white;
      align-self: flex-end;
      border-bottom-right-radius: 4px;
    }
    .bot {
      background: #e5e7eb;
      color: black;
      align-self: flex-start;
      border-bottom-left-radius: 4px;
    }
    .time {
      font-size: 10px;
      opacity: 0.6;
      margin-top: 4px;
      text-align: right;
    }
    .clear-btn {
      background: #ef4444;
      padding: 5px 10px;
      border-radius: 10px;
      color: white;
      cursor: pointer;
      font-size: 13px;
    }
  </style>
</head>
<body>
  <div class="chat-container">
    <header>
      جمعتنا
      <div class="clear-btn" onclick="clearChat()">مسح</div>
    </header>
    <main id="chat"></main>
    <footer>
      <textarea id="input" rows="2" placeholder="اكتب رسالة..."></textarea>
      <button onclick="sendMessage()">إرسال</button>
    </footer>
  </div>

  <script>
    const chat = document.getElementById('chat');
    const input = document.getElementById('input');

    // تحميل الرسائل من localStorage
    let messages = JSON.parse(localStorage.getItem('jamtna_messages') || '[]');
    messages.forEach(msg => addMessageToDOM(msg));

    function addMessageToDOM(msg) {
      const div = document.createElement('div');
      div.className = 'message ' + msg.from;
      div.innerHTML = `<div>${msg.text}</div><div class="time">${new Date(msg.time).toLocaleTimeString('ar‑EG',{hour:'2‑digit',minute:'2‑digit'})}</div>`;
      chat.appendChild(div);
      chat.scrollTop = chat.scrollHeight;
    }

    function sendMessage() {
      const text = input.value.trim();
      if (!text) return;
      const msg = { from: 'me', text, time: Date.now() };
      messages.push(msg);
      localStorage.setItem('jamtna_messages', JSON.stringify(messages));
      addMessageToDOM(msg);
      input.value = '';

      // رد تلقائي بعد 700ms
      setTimeout(() => {
        const botMsg = { from: 'bot', text: `رد تلقائي: استلمت "${text}"`, time: Date.now() };
        messages.push(botMsg);
        localStorage.setItem('jamtna_messages', JSON.stringify(messages));
        addMessageToDOM(botMsg);
      }, 700);
    }

    function clearChat() {
      if (!confirm('مسح المحادثة؟')) return;
      messages = [];
      localStorage.removeItem('jamtna_messages');
      chat.innerHTML = '';
    }

    // إرسال بالضغط على Enter
    input.addEventListener('keydown', function(e) {
      if (e.key === 'Enter' && !e.shiftKey) {
        e.preventDefault();
        sendMessage();
      }
    });
  </script>
</body>
</html>
