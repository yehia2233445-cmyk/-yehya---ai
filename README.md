<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>وصلة | برنامج الدردشة</title>

  <style>
    * {
      box-sizing: border-box;
    }

    :root {
      --bg: #0b1120;
      --panel: #111b2e;
      --panel2: #19263b;
      --accent: #38d9c4;
      --text: #f1f5f9;
      --muted: #9aabc1;
      --border: #27364d;
    }

    body {
      margin: 0;
      min-height: 100vh;
      padding: 20px;
      background: var(--bg);
      color: var(--text);
      font-family: Tahoma, Arial, sans-serif;
    }

    button, input {
      font: inherit;
    }

    button {
      cursor: pointer;
    }

    .app {
      max-width: 1100px;
      height: min(760px, calc(100vh - 40px));
      min-height: 540px;
      margin: auto;
      display: grid;
      grid-template-columns: 310px 1fr;
      background: var(--panel);
      border: 1px solid var(--border);
      border-radius: 20px;
      overflow: hidden;
      box-shadow: 0 20px 60px #0004;
    }

    aside {
      background: #0f192a;
      border-left: 1px solid var(--border);
      padding: 20px;
      min-width: 0;
    }

    .brand {
      font-size: 26px;
      font-weight: bold;
      color: var(--accent);
      margin-bottom: 8px;
    }

    .subtitle {
      color: var(--muted);
      font-size: 13px;
      margin-bottom: 22px;
    }

    .profile {
      display: flex;
      align-items: center;
      gap: 10px;
      padding: 12px;
      border-radius: 12px;
      background: var(--panel2);
      margin-bottom: 18px;
    }

    .avatar {
      width: 43px;
      height: 43px;
      border-radius: 50%;
      background: #264c65;
      display: grid;
      place-items: center;
      font-size: 21px;
      flex-shrink: 0;
    }

    .profile small, .contact small {
      display: block;
      color: var(--muted);
      margin-top: 5px;
      font-size: 12px;
    }

    .list-heading {
      display: flex;
      align-items: center;
      justify-content: space-between;
      margin: 20px 0 12px;
    }

    .new-chat {
      border: 0;
      background: var(--accent);
      color: #08221f;
      border-radius: 9px;
      padding: 7px 12px;
      font-weight: bold;
    }

    #contacts {
      display: flex;
      flex-direction: column;
      gap: 7px;
      overflow-y: auto;
      max-height: 65%;
    }

    .contact {
      width: 100%;
      text-align: right;
      display: flex;
      align-items: center;
      gap: 10px;
      border: 1px solid transparent;
      color: var(--text);
      background: transparent;
      padding: 11px 9px;
      border-radius: 12px;
    }

    .contact.active {
      background: var(--panel2);
      border-color: #31445d;
    }

    .contact:hover {
      background: #19283d;
    }

    .contact-info {
      min-width: 0;
      flex: 1;
    }

    .contact-info strong {
      display: block;
    }

    .contact-info small {
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
    }

    main {
      display: flex;
      flex-direction: column;
      min-width: 0;
    }

    .chat-header {
      padding: 17px 22px;
      border-bottom: 1px solid var(--border);
      display: flex;
      align-items: center;
      gap: 12px;
      min-height: 80px;
    }

    .chat-header .title {
      font-weight: bold;
    }

    .chat-header small {
      display: block;
      color: var(--muted);
      margin-top: 5px;
    }

    #messages {
      flex: 1;
      overflow-y: auto;
      padding: 24px;
      display: flex;
      flex-direction: column;
      gap: 16px;
    }

    .welcome {
      margin: auto;
      text-align: center;
      color: var(--muted);
      line-height: 1.9;
    }

    .welcome .big {
      font-size: 48px;
    }

    .message {
      max-width: 78%;
      display: flex;
      flex-direction: column;
      gap: 6px;
      align-self: flex-start;
    }

    .message.mine {
      align-self: flex-end;
    }

    .bubble {
      padding: 12px 15px;
      border-radius: 15px 15px 4px 15px;
      background: #223149;
      overflow-wrap: anywhere;
      white-space: pre-wrap;
      line-height: 1.7;
    }

    .mine .bubble {
      background: #087f79;
      border-radius: 15px 15px 15px 4px;
    }

    .meta {
      color: var(--muted);
      font-size: 11px;
      padding: 0 4px;
    }

    .composer {
      padding: 16px;
      border-top: 1px solid var(--border);
      display: flex;
      gap: 10px;
    }

    #messageInput {
      flex: 1;
      min-width: 0;
      border: 1px solid var(--border);
      background: #0c1525;
      color: white;
      border-radius: 12px;
      padding: 14px;
      outline: none;
    }

    #messageInput:focus {
      border-color: var(--accent);
    }

    #sendButton {
      border: 0;
      background: var(--accent);
      color: #08221f;
      font-weight: bold;
      border-radius: 12px;
      padding: 0 20px;
    }

    .note {
      font-size: 11px;
      color: var(--muted);
      text-align: center;
      padding: 0 12px 12px;
    }

    @media (max-width: 650px) {
      body {
        padding: 0;
      }

      .app {
        width: 100%;
        height: 100dvh;
        min-height: 480px;
        border-radius: 0;
        grid-template-columns: 105px minmax(0, 1fr);
      }

      aside {
        padding: 10px 6px;
      }

      .brand {
        font-size: 19px;
        text-align: center;
      }

      .subtitle {
        font-size: 10px;
        text-align: center;
      }

      .profile {
        padding: 8px 3px;
        flex-direction: column;
        text-align: center;
        font-size: 12px;
        gap: 4px;
      }

      .profile small {
        font-size: 10px;
      }

      .list-heading {
        flex-direction: column;
        gap: 8px;
        font-size: 12px;
      }

      .new-chat {
        padding: 7px;
        font-size: 12px;
      }

      .contact {
        padding: 8px 3px;
        flex-direction: column;
        text-align: center;
        gap: 4px;
      }

      .contact .avatar {
        width: 35px;
        height: 35px;
        font-size: 17px;
      }

      .contact-info strong {
        font-size: 11px;
      }

      .contact-info small {
        max-width: 90px;
        font-size: 10px;
      }

      .chat-header {
        padding: 12px 8px;
        gap: 7px;
      }

      .chat-header .avatar {
        width: 35px;
        height: 35px;
      }

      .chat-header .title {
        font-size: 13px;
      }

      .chat-header small {
        font-size: 10px;
      }

      #messages {
        padding: 12px 8px;
      }

      .message {
        max-width: 92%;
      }

      .bubble {
        font-size: 13px;
        padding: 10px;
      }

      .composer {
        padding: 8px;
        gap: 5px;
      }

      #messageInput {
        padding: 10px 7px;
        font-size: 12px;
      }

      #sendButton {
        padding: 0 10px;
        font-size: 12px;
      }
    }
  </style>
</head>

<body>
  <div class="app">

    <aside>
      <div class="brand">وصلة 💬</div>
      <div class="subtitle">مساحتك للمحادثات</div>

      <div class="profile">
        <div class="avatar">👤</div>
        <div>
          <strong>أنت</strong>
          <small>حساب تجريبي</small>
        </div>
      </div>

      <div class="list-heading">
        <strong>المحادثات</strong>
        <button class="new-chat" id="newChat">+ جديد</button>
      </div>

      <div id="contacts"></div>
    </aside>

    <main>
      <header class="chat-header">
        <div class="avatar" id="headerAvatar">👋</div>
        <div>
          <div class="title" id="headerName">أهلًا بك!</div>
          <small id="headerStatus">اختر محادثة للبدء</small>
        </div>
      </header>

      <section id="messages" aria-live="polite">
        <div class="welcome">
          <div class="big">💬</div>
          <h2>مرحبًا بك في وصلة</h2>
          <p>اختر محادثة من القائمة،<br>أو أنشئ محادثة جديدة.</p>
        </div>
      </section>

      <form class="composer" id="chatForm">
        <input
          id="messageInput"
          type="text"
          placeholder="اكتب رسالتك هنا..."
          maxlength="2000"
          autocomplete="off"
          aria-label="نص الرسالة"
        >
        <button id="sendButton" type="submit">إرسال ➤</button>
      </form>

      <div class="note">
        نسخة تجريبية: الرسائل محفوظة في هذا المتصفح فقط.
      </div>
    </main>

  </div>

  <script>
    const contactsElement = document.getElementById("contacts");
    const messagesElement = document.getElementById("messages");
    const chatForm = document.getElementById("chatForm");
    const messageInput = document.getElementById("messageInput");

    const headerName = document.getElementById("headerName");
    const headerAvatar = document.getElementById("headerAvatar");
    const headerStatus = document.getElementById("headerStatus");

    const defaultChats = [
      {
        id: 1,
        name: "أحمد",
        avatar: "🧑",
        messages: [
          {
            text: "أهلًا! دي أول محادثة تجريبية 👋",
            mine: false,
            time: "10:00 ص"
          },
          {
            text: "أهلًا بيك! سعيد بتجربة البرنامج 😄",
            mine: true,
            time: "10:01 ص"
          }
        ]
      },
      {
        id: 2,
        name: "محمد",
        avatar: "👨",
        messages: [
          {
            text: "إزيك؟ عامل إيه؟",
            mine: false,
            time: "11:15 ص"
          }
        ]
      },
      {
        id: 3,
        name: "فريق التطوير",
        avatar: "👨‍💻",
        messages: [
          {
            text: "مرحبًا بك في مشروعنا الجديد!",
            mine: false,
            time: "12:30 م"
          }
        ]
      }
    ];

    function loadChats() {
      try {
        const saved = localStorage.getItem("wasla_chats");
        if (saved) {
          const parsed = JSON.parse(saved);
          if (Array.isArray(parsed)) return parsed;
        }
      } catch (error) {
        console.warn("تعذر تحميل المحادثات المحفوظة.");
      }

      return defaultChats.map(chat => ({
        ...chat,
        messages: chat.messages.map(message => ({ ...message }))
      }));
    }

    let chats = loadChats();
    let activeChatId = chats.length ? chats[0].id : null;
    let nextId = Math.max(0, ...chats.map(chat => chat.id)) + 1;

    function saveChats() {
      try {
        localStorage.setItem("wasla_chats", JSON.stringify(chats));
      } catch (error) {
        console.warn("تعذر حفظ المحادثات على هذا الجهاز.");
      }
    }

    function getActiveChat() {
      return chats.find(chat => chat.id === activeChatId);
    }

    function renderContacts() {
      contactsElement.replaceChildren();

      chats.forEach(chat => {
        const button = document.createElement("button");
        button.className =
          "contact" + (chat.id === activeChatId ? " active" : "");

        const avatar = document.createElement("div");
        avatar.className = "avatar";
        avatar.textContent = chat.avatar;

        const info = document.createElement("div");
        info.className = "contact-info";

        const name = document.createElement("strong");
        name.textContent = chat.name;

        const preview = document.createElement("small");
        const lastMessage = chat.messages[chat.messages.length - 1];
        preview.textContent = lastMessage
          ? (lastMessage.mine ? "أنت: " : "") + lastMessage.text
          : "ابدأ المحادثة";

        info.append(name, preview);
        button.append(avatar, info);

        button.addEventListener("click", () => {
          activeChatId = chat.id;
          render();
        });

        contactsElement.appendChild(button);
      });
    }

    function renderMessages() {
      messagesElement.replaceChildren();

      const chat = getActiveChat();

      if (!chat) {
        const welcome = document.createElement("div");
        welcome.className = "welcome";
        welcome.textContent = "أنشئ محادثة جديدة للبدء 💬";
        messagesElement.appendChild(welcome);
        return;
      }

      if (chat.messages.length === 0) {
        const welcome = document.createElement("div");
        welcome.className = "welcome";
        welcome.textContent = "لا توجد رسائل بعد. ابدأ الحديث!";
        messagesElement.appendChild(welcome);
      }

      chat.messages.forEach(message => {
        const wrapper = document.createElement("div");
        wrapper.className = "message" + (message.mine ? " mine" : "");

        const bubble = document.createElement("div");
        bubble.className = "bubble";
        bubble.textContent = message.text;

        const meta = document.createElement("div");
        meta.className = "meta";
        meta.textContent =
          (message.mine ? "أنت" : chat.name) + " · " + message.time;

        wrapper.append(bubble, meta);
        messagesElement.appendChild(wrapper);
      });

      messagesElement.scrollTop = messagesElement.scrollHeight;
    }

    function render() {
      const chat = getActiveChat();

      if (chat) {
        headerName.textContent = chat.name;
        headerAvatar.textContent = chat.avatar;
        headerStatus.textContent = "محادثة تجريبية";
      } else {
        headerName.textContent = "أهلًا بك!";
        headerAvatar.textContent = "👋";
        headerStatus.textContent = "اختر محادثة للبدء";
      }

      renderContacts();
      renderMessages();
    }

    function getCurrentTime() {
      return new Intl.DateTimeFormat("ar-EG", {
        hour: "2-digit",
        minute: "2-digit"
      }).format(new Date());
    }

    chatForm.addEventListener("submit", event => {
      event.preventDefault();

      const text = messageInput.value.trim();
      const chat = getActiveChat();

      if (!text || !chat) return;

      chat.messages.push({
        text: text,
        mine: true,
        time: getCurrentTime()
      });

      messageInput.value = "";
      saveChats();
      render();

      messageInput.focus();
    });

    document.getElementById("newChat").addEventListener("click", () => {
      const name = prompt("اكتب اسم المحادثة الجديدة:");

      if (!name || !name.trim()) return;

      const cleanName = name.trim().slice(0, 40);

      const exists = chats.some(
        chat => chat.name.toLowerCase() === cleanName.toLowerCase()
      );

      if (exists) {
        alert("الاسم ده موجود بالفعل في القائمة.");
        return;
      }

      const newChat = {
        id: nextId++,
        name: cleanName,
        avatar: "🙂",
        messages: []
      };

      chats.push(newChat);
      activeChatId = newChat.id;

      saveChats();
      render();
      messageInput.focus();
    });

    render();
  </script>
</body>
</html>
