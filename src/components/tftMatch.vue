<template>
  <div class="container">
    <div class="text-center m-2">
      <img src="../assets/images/set-4-logo.png" class="w-25 img-fluid" />
    </div>
    <div class="d-flex justify-content-center align-items-center">
      <div class="container">
        <div class="row">
          <div class="col-12">
            <div class="card mb-3 text-white bg-tft border-primary">
              <div class="card-body">
                <div class="card-text">
                  <ul class="list-group text-left text-white">
                    <li>
                      😉<i> Enter all the players in the game, except you.</i>
                    </li>
                    <li>
                      ⚔️<i>
                        At the start after the fourth game, you will have the
                        possible next opponents.</i
                      >
                    </li>
                    <li>
                      💀<i>
                        When a player dies, you must remove them from the list
                        to restart the cycle.</i
                      >
                    </li>
                    <li>👊<i> Have fun and win the match.</i></li>
                  </ul>
                </div>
              </div>
            </div>
          </div>
          <div class="col-4">
            <div class="card text-white bg-tft border-primary">
              <h5 class="card-header text-center">Enter Match Players (7)</h5>
              <div class="card-body">
                <div class="card-text">
                  <div id="bx-players" class="form-inline">
                    <input
                      v-model="player"
                      v-on:keyup.enter="addPlayer(player)"
                      placeholder="Summoner Name"
                      class="form-control m-1"
                      style="width:11em;"
                    />
                    <button
                      class="btn btn-light"
                      v-on:click="addPlayer(player)"
                    >
                      <i class="material-icons align-middle">add</i>
                    </button>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="col-4">
            <div class="card text-white bg-tft border-primary">
              <h5 class="card-header text-center">Select Current Match</h5>
              <div class="card-body">
                <div class="card-text">
                  <div
                    v-for="(playerInMatch, index) in playersInMatch"
                    :key="index"
                    id="bx-players"
                    class="form-group align-center text-center"
                  >
                    <button
                      type="button"
                      class="btn btn-light m-1"
                      v-on:click="nextMatch(playerInMatch)"
                    >
                      {{ playerInMatch }}
                    </button>
                    <button
                      type="button"
                      class="btn btn-danger m-1"
                      v-on:click="deletePlayer(playerInMatch)"
                    >
                      <i class="tiny material-icons align-middle">clear</i>
                    </button>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="col-4">
            <div class="card text-white bg-tft border-primary">
              <h5 class="card-header text-center">Probably Match</h5>
              <div class="card-body">
                <div class="card-text">
                  <div
                    v-for="(probMatch, index) in probablyMatch"
                    :key="index"
                    id="bx-players"
                    class="form-group align-center text-center"
                  >
                    <button type="button" class="btn btn-primary" disabled>
                      {{ probMatch }}
                    </button>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="card mt-2 mb-3 text-white bg-tft border-primary mb-2">
          <h5 class="card-header text-center">Match History</h5>
          <div class="card-body">
            <div class="card-text">
              <ul class="list-inline">
                <li
                  class="list-group-item bg-tft border-0"
                  v-for="(playerMatch, index) in fullHistoryMatch"
                  :key="index"
                >
                  <button type="button" class="btn btn-primary" disabled>
                    {{ playerMatch }}
                  </button>
                </li>
              </ul>
            </div>
            <button
              type="button"
              class="btn btn-light m-1"
              v-on:click="reload()"
            >
              New Match
              <i class="tiny material-icons align-middle">refresh</i>
            </button>
          </div>
          <div class="card-footer">
           <a href="https://github.com/Maaato/tftMatch" class="text-white"><img src="../assets/images/GitHub-Mark-32px.png" class="img-fluid mr-2" />Made by Maaato</a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      player: null,
      playersInMatch: [],
      Matchs: [],
      probablyMatch: [],
      fullHistoryMatch: [],
      countMatchs: 4,
    };
  },
  methods: {
    addPlayer: function(player) {
      if (this.playersInMatch.length >= 7) return false;
      if (player === null || player === undefined || player === "")
        return false;
      let findPlayer = this.playersInMatch.find((p) => p == player);
      if (findPlayer === null || findPlayer === undefined)
        this.playersInMatch.push(player);
      this.player = null;
      return;
    },
    deletePlayer: function(playerInMatch) {
      let i = this.playersInMatch.indexOf(playerInMatch);
      if (i !== -1) this.playersInMatch.splice(i, 1);
      this.Matchs = [];
      this.probablyMatch = [];
      switch (true) {
        case this.playersInMatch.length == 6 || this.playersInMatch.length == 4:
          this.countMatchs = 3;
          break;
        case this.playersInMatch.length == 5:
          this.countMatchs = 4;
          break;
        case this.playersInMatch.length == 3:
          this.countMatchs = 2;
          break;
        case this.playersInMatch.length == 2:
          this.countMatchs = 1;
          break;
      }
    },
    nextMatch: function(playerSlected) {
      this.fullHistoryMatch.push(playerSlected);
      if (this.Matchs.length < this.countMatchs) {
        this.Matchs.push(playerSlected);
      } else if (this.Matchs.length == this.countMatchs) {
        this.Matchs.shift();
        this.Matchs.push(playerSlected);
        this.probablyMatch = [];
      }
      if (this.Matchs.length == this.countMatchs) {
        for (let i = 0; i < this.playersInMatch.length; i++) {
          for (let x = 0; x < this.Matchs.length; x++) {
            let f = this.Matchs.find((p) => p == this.playersInMatch[i]);
            if (!f) {
              this.probablyMatch.push(this.playersInMatch[i]);
              break;
            }
          }
        }
      }
    },
    reload: function() {
      this.countMatchs = 4;
      this.fullHistoryMatch = [];
      this.Matchs = [];
      this.playersInMatch = [];
      this.probablyMatch = [];
      this.player = null;
    },
  },
};
</script>
