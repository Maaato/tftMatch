<template>
  <div class="container">
    <div class="text-center">
      <img
        src="https://vignette.wikia.nocookie.net/leagueoflegends/images/1/1e/Teamfight_Tactics_logo.png/revision/latest?cb=20200307230923"
        class="img-fluid w-25"
      />
    </div>
    <div class="d-flex justify-content-center align-items-center">
      <div class="container">
        <div class="row">
          <div class="col-md-5 offset-md-4">
            <div class="card text-white bg-tft border-dark">
              <div class="card-body">
                <div class="card-text">
                  <div class="form-inline">
                    <input
                      v-model="newPlayer"
                      v-on:keyup.enter="nwPlayer(newPlayer)"
                      placeholder="Summoner Name"
                      class="form-control mr-2"
                    />
                    <button
                      class="btn btn-primary mr-4"
                      v-on:click="nwPlayer(newPlayer)"
                    >
                      <i class="material-icons align-middle">add</i>
                    </button>
                    <div v-if="checked ==false">
                      <label class="checkbox-inline text-white"><input type="checkbox" v-model="checked" class="form-check-input mr-2">me?</label>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="row mt-2">
          <div class="col-4">
            <div
              class="card text-white bg-success mb-3"
              style="max-width: 18rem;"
            >
              <div class="card-body">
                <h5 class="card-title"></h5>
                <p class="card-text">
                  Some quick example text to build on the card title and make up
                  the bulk of the card's content.
                </p>
              </div>
            </div>
          </div>
          <div class="col-4">
            <div
              class="card text-white bg-success mb-3"
              style="max-width: 18rem;"
            >
              <div class="card-body">
                <h5 class="card-title">{{playersInMatch[0]}}</h5>
                <p class="card-text">
                  Some quick example text to build on the card title and make up
                  the bulk of the card's content.
                </p>
              </div>
            </div>
          </div>
          <div class="col-4">
            <div
              class="card text-white bg-success mb-3"
              style="max-width: 18rem;"
            >
              <div class="card-body">
                <h5 class="card-title">{{playersInMatch[1]}}</h5>
                <p class="card-text">
                  Some quick example text to build on the card title and make up
                  the bulk of the card's content.
                </p>
              </div>
            </div>
          </div>
          <div class="col-4">
            <div
              class="card text-white bg-success mb-3"
              style="max-width: 18rem;"
            >
              <div class="card-body">
                <h5 class="card-title">{{playersInMatch[6]}}</h5>
                <p class="card-text">
                  Some quick example text to build on the card title and make up
                  the bulk of the card's content.
                </p>
              </div>
            </div>
          </div>
          <div class="col-4"></div> <!-- center -->
          <div class="col-4">
            <div
              class="card text-white bg-success mb-3"
              style="max-width: 18rem;"
            >
              <div class="card-body">
                <h5 class="card-title">{{playersInMatch[2]}}</h5>
                <p class="card-text">
                  Some quick example text to build on the card title and make up
                  the bulk of the card's content.
                </p>
              </div>
            </div>
          </div>
          <div class="col-4">
            <div
              class="card text-white bg-success mb-3"
              style="max-width: 18rem;"
            >
              <div class="card-body">
                <h5 class="card-title">{{playersInMatch[5]}}</h5>
                <p class="card-text">
                  Some quick example text to build on the card title and make up
                  the bulk of the card's content.
                </p>
              </div>
            </div>
          </div>
          <div class="col-4">
            <div
              class="card text-white bg-success mb-3"
              style="max-width: 18rem;"
            >
              <div class="card-body">
                <h5 class="card-title">{{playersInMatch[4]}}</h5>
                <p class="card-text">
                  Some quick example text to build on the card title and make up
                  the bulk of the card's content.
                </p>
              </div>
            </div>
          </div>
          <div class="col-4">
            <div
              class="card text-white bg-success mb-3"
              style="max-width: 18rem;"
            >
              <div class="card-body">
                <h5 class="card-title">{{playersInMatch[3]}}</h5>
                <p class="card-text">
                  Some quick example text to build on the card title and make up
                  the bulk of the card's content.
                </p>
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
                  <button type="button" class="btn btn-primary" disabled>
                    {{ playerMatch }}
                  </button>
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
      newPlayer: null,
      playersInMatch: [],
      historyMatch: [],
      probablyMatch: [],
      fullHistoryMatch: [],
      eliminatedPlayer: false,
      c: 4,
    };
  },
  methods: {
    nwPlayer: function(newPlayer) {
      if (this.playersInMatch.length >= 7) return false;
      if (newPlayer === null || newPlayer === undefined || newPlayer === "")
        return false;
      let f = this.playersInMatch.find((x) => x == newPlayer);
      if (f === null || f === undefined) {
        if(this.checked == true) this.checked = false;
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
        console.log("aki toi x1");
        this.historyMatch.push(playerSlected);
      } else if (this.historyMatch.length == this.c) {
        console.log("aki toi x2");
        if (this.historyMatch[0] === "BOT") {
          console.log("aki toi x3");
          this.historyMatch.shift();
          this.historyMatch.push("BOT");
        }
        this.historyMatch.shift();
        this.historyMatch.push(playerSlected);
        this.probablyMatch = [];
      }
      if (this.historyMatch.length == this.c) {
        for (let i = 0; i < this.playersInMatch.length; i++) {
          for (let x = 0; x < this.historyMatch.length; x++) {
            let f = this.historyMatch.find((p) => p == this.playersInMatch[i]);
            if (!f && !this.probablyMatch.length < 4) {
              this.probablyMatch.push(this.playersInMatch[i]);
              break;
            }
          }
        }
      }
      console.log(`-- Next Match Lenght --`);
      console.log(`this.playersInMatch.length : ${this.playersInMatch.length}`);
      console.log(`this.historyMatch.length : ${this.historyMatch.length}`);
      console.log(`this.probablyMatch.length : ${this.probablyMatch.length}`);
      console.log(`-- Next Match DATA--`);
      console.log(`this.playersInMatch.length : ${this.playersInMatch}`);
      console.log(`this.historyMatch.length : ${this.historyMatch}`);
      console.log(`this.probablyMatch.length : ${this.probablyMatch}`);
      console.log(`this.c : ${this.c}`);
      console.log(`this.checked : ${this.checked}`)
    },
    eliPlayer: function(playerInMatch) {
      let i = this.playersInMatch.indexOf(playerInMatch);
      if (i !== -1) {
        this.playersInMatch.splice(i, 1);
        this.eliminatedPlayer = true;
      }
      this.historyMatch = [];
      this.probablyMatch = [];
      if (this.playersInMatch.length <= 4) this.c--;
    },
  },
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
