<template>
  <div class="home">
    <div v-if="isAuth">
      Приветствую вас, уважаемый <b>{{ userName }}</b>
      <div class="save_btn">
        <button class="glow-on-hover" @click="logout">Выйти</button>
      </div>
    </div>
    <div v-else>
      <label>Введите имя:</label>

      <input v-model="userName" type="text" />
      <div class="save_btn">
        <button class="glow-on-hover" @click="login">Сохранить</button>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "HomePage",
  data() {
    return {
      isAuth: false,
      userName: "",
    };
  },
  created() {
    if (localStorage.getItem("isAuth")) {
      this.isAuth = true;
      this.userName = localStorage.getItem("userName");
    }
  },
  methods: {
    login() {
      if (this.userName !== "") {
        console.log(this.userName);
        this.isAuth = true;
        localStorage.setItem("isAuth", true);
        localStorage.setItem("userName", this.userName);

        this.$router.push({
          name: "Chat",
          query: { username: this.userName },
        });
      } else {
        console.log("Данные введи быстро");
      }
    },
    logout() {
      this.isAuth = false;
      this.userName = "";
      localStorage.removeItem("userName");
      localStorage.removeItem("isAuth");
    },
  },
};
</script>
<style>
.save_btn {
  justify-content: center;
  display: flex;
  margin-top: 10px;
}
input {
  border-radius: 10px;
}
label {
  margin-right: 10px;
}
.home {
  padding-top: 30px;
  justify-content: center;
  display: flex;

  background: #a28089;
}
.glow-on-hover {
  margin: 10px;
  width: 150px;
  height: 40px;
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
</style>
