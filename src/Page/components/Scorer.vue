<template>
  <div class="content" onselectstart="return false" @click="Add()" @contextmenu.prevent="Sub()">
    <div class="top">
      <div v-for="i in 14" :key="i" class="dot" :class="{LedBright:HLed(i)}"></div>
    </div>
    <div class="center">
      <div class="LVerticalLine">
        <div v-for="i in 70" :key="i" class="dot" :class="{LedBright:VLed(i)}"></div>
      </div>
      <div class="ScoreOuterFrame">
        <div v-for="i in 15" :key="i" class="ScoreBox" :class="{ScoreBright:i<=Score}">
          <span class="Score">{{i}}</span>
        </div>
        <div class="PassLine"></div>
        <div v-for="i in 5" :key="i+15" class="ScoreBox" :class="{PassScoreBright :(i+15)<=Score}">
          <span class="Score">{{i+15}}</span>
        </div>
      </div>
      <div class="RVerticalLine">
        <div v-for="i in 70" :key="i" class="dot" :class="{LedBright:VLed(i)}"></div>
      </div>
    </div>
    <div class="bottom">
      <div v-for="i in 14" :key="i" class="dot" :class="{LedBright:HLed(i)}"></div>
    </div>
    <audio :src="Passm" style="display:none" ref="Pass" muted></audio>
    <audio :src="NoPassm" style="display:none" ref="NoPass" muted></audio>
  </div>
</template>

<script>
let Pass = require("../../assets/Pass.mp3");
let NoPass = require("../../assets/NoPass.mp3");
export default {
  props: ["passledinterval"],
  data() {
    return {
      Score: 0,
      EnableLed: false,
      H: "11111001111100",
      V:
        "1111100111110011111001111100111110011111001111100111110011111001111100",
      Passm: Pass,
      NoPassm: NoPass
    };
  },
  methods: {
    Add() {
      if (this.Score < 20) {
        this.Score++;
        if (this.Score === 1) {
          setTimeout(() => {
            try {
              if (this.Score < 16) {
                var audio = this.$refs.NoPass;
                audio.play();
              }
            } catch (ex) {
              alert(ex);
            }
          }, 5000);
        }
        if (this.Score === 16) {
          try {
            var NoPassaudio = this.$refs.NoPass;
            NoPassaudio.pause();
            NoPassaudio.currentTime = 0;
            var Passaudio = this.$refs.Pass;
            Passaudio.play();
            // audio.cloneNode().play();
          } catch (ex) {
            alert(ex);
          }
          this.EnableLed = true;
          setInterval(() => {
            this.Pass();
          }, this.passledinterval);
        }
      }
    },
    Sub() {
      if (this.Score > 0) {
        this.Score--;
        if (this.Score == 15) {
          try {
            var highestTimeoutId = setTimeout(";");
            for (var i = 0; i < highestTimeoutId; i++) {
              clearTimeout(i);
            }
            var Passaudio = this.$refs.Pass;
            Passaudio.pause();
            Passaudio.currentTime = 0;
            var NoPassaudio = this.$refs.NoPass;
            NoPassaudio.play();
          } catch (ex) {
            alert(ex);
          }
          this.EnableLed = false;
        }
      }
    },
    Reset() {
      this.Score = 0;
      this.EnableLed = false;
    },
    keyFunction() {
      if (event.keyCode == 32) {
        this.Add();
        return false;
      }
    },
    Pass() {
      // debugger;
      this.H =
        this.H.substr(this.H.length - 1, 1) +
        this.H.substr(0, this.H.length - 1);
      this.V =
        this.V.substr(this.V.length - 1, 1) +
        this.V.substr(0, this.V.length - 1);
    },
    HLed(i) {
      if (!this.EnableLed) {
        return false;
      }
      return this.H.split("")[i - 1] == "1" ? true : false;
    },
    VLed(i) {
      if (!this.EnableLed) {
        return false;
      }
      return this.V.split("")[i - 1] == "1" ? true : false;
    }
  },
  computed: {},
  watch: {},
  created() {
    document.onkeydown = this.keyFunction;
  },
  mounted() {}
};
</script>
<style lang="scss" scoped>
.content {
  background-color: rgb(167, 152, 113);
  display: flex;
  flex-direction: column;
  width: 140px;
}
.top {
  display: flex;
  z-index: 1;
}
.center {
  display: flex;
}
.bottom {
  display: flex;
  flex-direction: row-reverse;
}
.LVerticalLine {
  z-index: 1;
  display: flex;
  flex-direction: column-reverse;
}
.RVerticalLine {
  display: flex;
  flex-direction: column;
}
.dot {
  background-color: rgb(228, 189, 130);
  width: 8px;
  height: 8px;
  border-radius: 50%;
  margin: 1px;
}
.ScoreOuterFrame {
  background-color: rgb(167, 152, 113);
  width: 120px;
  height: 685px;
  display: flex;
  flex-direction: column-reverse;
  align-content: center;
  padding-top: 3px;
  padding-bottom: 3px;
  font-family: "Microsoft JhengHei";
}
.ScoreBox {
  background-color: rgb(132, 132, 142);
  width: 110px;
  height: 60px;
  margin: 2px auto 2px;
  border-radius: 20px;
  display: flex;
  justify-content: center;
  align-content: center;
}
.Score {
  font-size: 22px;
  margin: auto;
}
.ScoreBright {
  background-color: rgb(250, 250, 250);
  box-shadow: 0px 0px 30px 5px rgba(250, 250, 250, 0.8);
}
.PassLine {
  z-index: 1;
  border-top: 2px dashed #ff0000;
  height: 1px;
  overflow: hidden;
  box-shadow: 0px 0px 35px 2px rgba(255, 0, 0, 0.8);
}
.LedBright {
  background-color: rgb(250, 250, 250);
  box-shadow: 0px 0px 30px 2px rgb(245, 231, 42);
}
.PassScoreBright {
  background-color: rgb(250, 70, 70);
  box-shadow: 0px 0px 20px 5px rgba(255, 120, 139, 0.8);
}
</style>