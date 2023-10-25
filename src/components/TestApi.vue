<template>
  <div class="teams">
    <div>
      <h1>Игровые команды NBA</h1>
    </div>
    <div class="teams_api" v-if="isLoad">
      <h2>Пожалуйста, подождите..</h2>
    </div>
    <div v-else class="teams_api">
      <div v-for="el in gamesData" :key="el.id">
        {{ el.id }}. {{ el.abbreviation }} {{ el.city }}
        <img
          src="https://espicture.ru/800/600/http/cdn.onlinewebfonts.com/svg/download_229056.png"
          style="width: 20px; height: 15px"
          alt="delete"
          @click="removeTeam(el.id)"
        />
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "TestApi",
  data() {
    return {
      gamesData: [],
      isLoad: true,
    };
  },
  mounted() {
    const url = "https://free-nba.p.rapidapi.com/teams?page=0";
    const options = {
      method: "GET",
      headers: {
        "X-RapidAPI-Key": "a13187ec7emshb949e2f08e6728ap16495cjsn264f75164330",
        "X-RapidAPI-Host": "free-nba.p.rapidapi.com",
      },
    };

    fetch(url, options)
      .then((res) => res.json())
      .then((res) => {
        console.log(res);
        this.gamesData = res.data;
        this.isLoad = false;
      });
    console.log(this.gamesData.data);
  },
  methods: {
    removeTeam(id) {
      this.gamesData = this.gamesData.filter((el) => el.id !== id);
    },
  },
};
</script>
<style>
.teams_api {
  justify-content: center;
  display: grid;
}
.teams {
  padding-top: 30px;
  justify-content: center;
  display: grid;

  background: #a28089;
}
</style>
