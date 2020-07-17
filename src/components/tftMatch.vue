<template>
  <div class="container">
    <div class="text-center">
      <img
        src="https://vignette.wikia.nocookie.net/leagueoflegends/images/1/1e/Teamfight_Tactics_logo.png/revision/latest?cb=20200307230923"
        class="img-fluid w-25 p-3"
      />
    </div>
    <div class="d-flex justify-content-center align-items-center">
      <div class="container">
        <div class="row">
          <div class="col-4">
            <div class="card text-white bg-tft border-dark">
              <h5 class="card-header text-center">Match Players (7)</h5>
              <div class="card-body">
                <div class="card-text">
                  <div id="bx-players" class="form-inline">
                    <input
                      v-model="newPlayer"
                      v-on:keyup.enter="nwPlayer(newPlayer)"
                      placeholder="Summoner Name"
                      class="form-control m-1" style="width:11em;"
                    />
                    <button class="btn btn-primary" v-on:click="nwPlayer(newPlayer)">
                      <i class="material-icons align-middle">add</i>
                    </button>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="col-4">
            <div class="card text-white bg-tft border-dark">
              <h5 class="card-header text-center">Select Current Match</h5>
              <div class="card-body">
                <div class="card-text">
                  <div
                    v-for="playerInMatch in playersInMatch"
                    :key="playerInMatch"
                    id="bx-players"
                    class="form-group align-center text-center"
                  >
                    <button
                      type="button"
                      class="btn btn-primary m-1"
                      v-on:click="nextMatch(playerInMatch)"
                    >{{playerInMatch}}</button>
                    <button
                      type="button"
                      class="btn btn-danger m-1"
                      v-on:click="eliPlayer(playerInMatch)"
                    >
                      <i class="tiny material-icons align-middle">delete</i>
                    </button>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="col-4">
            <div class="card text-white bg-tft border-dark">
              <h5 class="card-header text-center">Probably Match</h5>
              <div class="card-body">
                <div class="card-text">
                  <div
                    v-for="probMatch in probablyMatch"
                    :key="probMatch"
                    id="bx-players"
                    class="form-group align-center text-center"
                  >
                    <button type="button" class="btn btn-primary" disabled>{{probMatch}}</button>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="card mt-5 text-white bg-tft border-dark">
          <h5 class="card-header text-center">Match History</h5>
          <div class="card-body">
            <div class="card-text">
              <ul class="list-inline">
                <li
                  class="list-group-item bg-tft border-0"
                  v-for="playerMatch in fullHistoryMatch"
                  :key="playerMatch"
                >
                  <button type="button" class="btn btn-primary" disabled>{{playerMatch}}</button>
                </li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "TftMatch",
  data() {
    return {
      userName: null,
      newPlayer: null,
      playersInMatch: [],
      historyMatch: [],
      probablyMatch: [],
      fullHistoryMatch: [],
      c: 4
    };
  },
  methods: {
    nwPlayer: function(newPlayer) {
      if (this.playersInMatch.length >= 7) return false;
      if (newPlayer === null || newPlayer === undefined || newPlayer === "")
        return false;
      let f = this.playersInMatch.find(x => x == newPlayer);
      if (f === null || f === undefined) {
        this.playersInMatch.push(newPlayer);
        this.newPlayer = "";
        return;
      } else {
        return false;
      }
    },
    nextMatch: function(playerSlected) {
      this.fullHistoryMatch.push(playerSlected);
      if (this.historyMatch.length < this.c) {
        this.historyMatch.push(playerSlected);
      } else if (this.historyMatch.length == this.c) {
        this.historyMatch.shift();
        this.historyMatch.push(playerSlected);
        this.probablyMatch = [];
      }
      if (this.historyMatch.length == this.c) {
        for (let i = 0; i < this.playersInMatch.length; i++) {
          for (let x = 0; x < this.historyMatch.length; x++) {
            let encontrado = this.historyMatch.find(
              p => p == this.playersInMatch[i]
            );
            if (!encontrado) {
              this.probablyMatch.push(this.playersInMatch[i]);
              break;
            }
          }
        }
      }
      //console.log(`-- Next Match --`);
      //console.log(`this.playersInMatch.length : ${this.playersInMatch.length}`);
      //console.log(`this.historyMatch.length : ${this.historyMatch.length}`);
      //console.log(`this.probablyMatch.length : ${this.probablyMatch.length}`);
      //console.log(`this.c : ${this.c}`);
      
    },
    eliPlayer: function(playerInMatch) {
      let i = this.playersInMatch.indexOf(playerInMatch);
      if (i !== -1) this.playersInMatch.splice(i, 1);
      this.historyMatch = [];
      this.probablyMatch = [];
      if (this.playersInMatch.length <= 4) this.c--;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
