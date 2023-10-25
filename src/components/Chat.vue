<template>
  <div v-if="userName" class="chat_container">
    <div class="chat">
      <div v-show="emptyMsg" class="empty">Текущих сообщений нет</div>
      <div class="text" v-for="message in messages" :key="message.id">
        {{ message.user }}: {{ message.text }}
      </div>
    </div>
    <div class="send_container">
      <input
        placeholder="Введите сообщение.."
        class="inputMsg"
        v-model="newMessage"
      />
      <button class="save_btn glow-on-hover" @click="sendMessage">
        <h4 class="btn_words">Отправить</h4>
      </button>
      <button class="save_btn glow-on-hover" @click="delMessage">
        <h4 class="btn_words">Удалить</h4>
      </button>
    </div>
  </div>

  <div class="unAuth" v-else>
    <h2>
      Для авторизации перейдите по
      <router-link :to="{ name: 'Home' }">
        <span class="span">ссылке</span>
      </router-link>
    </h2>
  </div>
</template>
<script>
export default {
  name: "ChatComp",
  data() {
    return {
      messages: [],
      newMessage: "",
      emptyMsg: true,
      userName: localStorage.getItem("userName"),
    };
  },
  computed() {
    localStorage.setItem("userName", this.$route.query.userName);
  },
  methods: {
    sendMessage() {
      if (!this.userName) {
        this.userName = "Аноним";
      }
      if (this.newMessage !== "") {
        this.emptyMsg = false;
        console.log(this.newMessage);
        this.messages.push({
          id: new Date().getTime(),
          text: this.newMessage,
          user: this.userName,
        });
        this.saveChatRecords();
        this.mewMessage = "";
      } else {
        alert("Введите сообщение");
      }
    },
    saveChatRecords() {
      const records = this.messages;
      localStorage.setItem(
        `messages_${this.username}`,
        JSON.stringify(records)
      );
    },
    delMessage() {
      this.messages = [];
      localStorage.removeItem(
        `messages_${this.username}`,
        JSON.stringify(this.message)
      );
      this.emptyMsg = true;
    },
    loadChatRecords() {
      const records = JSON.parse(
        localStorage.getItem(`messages_${this.username}`)
      );
      if (records) {
        this.messages = records;
        this.emptyMsg = false;
      }
    },
  },
  created() {
    this.loadChatRecords();
  },
};
</script>
<style>
.span {
  color: #ff0000;
}
.unAuth {
  justify-content: center;
  align-items: center;
  display: grid;
}
.text {
  margin-left: 10px;
}
input {
  height: 25px;
  width: 300px;
}
.btn_words {
  margin-top: 5px;
}
.empty {
  margin-left: 400px;
  margin-top: 30px;
}
.save_btn {
  justify-content: center;
  display: flex;
  margin-top: 10px;
}
.glow-on-hover {
  margin: 10px;
  width: 150px;
  height: 30px;
  border: none;
  outline: none;
  color: #fff;
  background: #111;
  cursor: pointer;
  position: relative;
  z-index: 0;
  border-radius: 10px;
}

.glow-on-hover:before {
  content: "";
  background: linear-gradient(
    45deg,
    #ff0000,
    #ff7300,
    #fffb00,
    #48ff00,
    #00ffd5,
    #002bff,
    #7a00ff,
    #ff00c8,
    #ff0000
  );
  position: absolute;
  top: -2px;
  left: -2px;
  background-size: 400%;
  z-index: -1;
  filter: blur(5px);
  width: calc(100% + 4px);
  height: calc(100% + 4px);
  animation: glowing 20s linear infinite;
  opacity: 0;
  transition: opacity 0.3s ease-in-out;
  border-radius: 10px;
}

.glow-on-hover:active {
  color: #000;
}

.glow-on-hover:active:after {
  background: transparent;
}

.glow-on-hover:hover:before {
  opacity: 1;
}

.glow-on-hover:after {
  z-index: -1;
  content: "";
  position: absolute;
  width: 100%;
  height: 100%;
  background: #111;
  left: 0;
  top: 0;
  border-radius: 10px;
}

@keyframes glowing {
  0% {
    background-position: 0 0;
  }
  50% {
    background-position: 400% 0;
  }
  100% {
    background-position: 0 0;
  }
}
.chat {
  margin-top: 30px;
  width: 70%;
  padding-top: 30px;
  align-items: center;
  border-radius: 30px;
  border-width: 100px;
  border: 3px solid black;
  flex-direction: column;
}
.chat_container {
  display: grid;
  justify-items: center;
  grid-template-rows: 3fr 1fr;
  background: #a28089;
}
.send_container {
  align-items: center;
  display: flex;
  height: 30px;
  margin-top: 77px;
  margin-bottom: 50px;
}
</style>
