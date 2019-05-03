<template>
  <div class="content" @click="Add()">
    <div class="top">
      <div v-for="i in 14" :key="i" class="dot" :class="{GetScore:HLed(i)}"></div>
    </div>
    <div class="center">
      <div class="LVerticalLine">
        <div v-for="i in 69" :key="i" class="dot" :class="{GetScore:VLed(i)}"></div>
      </div>
      <div class="ScoreOuterFrame">
        <div v-for="i in 15" :key="i" class="ScoreBox" :class="{GetScore:i<=Score}">
          <span class="Score">{{i}}</span>
        </div>
        <div style="border-top:2px dashed #FF0000;height: 1px;overflow:hidden"></div>
        <div v-for="i in 5" :key="i+15" class="ScoreBox" :class="{GetPassScore:(i+15)<=Score}">
          <span class="Score">{{i+15}}</span>
        </div>
      </div>
      <div class="VerticalLine">
        <div v-for="i in 69" :key="i" class="dot" :class="{GetScore:VLed(i)}"></div>
      </div>
    </div>
    <div class="bottom">
      <div v-for="i in 14" :key="i" class="dot" :class="{GetScore:HLed(i)}"></div>
    </div>
    <!-- <audio id="audio" src="../../assets/NoPass.mp3" style="display:none" ref="aud" muted></audio>
    <input id="btn" type="button" value="zxc" @click="play()">-->
  </div>
</template>

<script>
export default {
  props: [],
  data() {
    return {
      Score: 0,
      k: 0
    };
  },
  methods: {
    Add() {
      if (this.Score < 20) {
        this.Score++;
        if (this.Score === 16) {
          setInterval(() => {
            this.Pass();
          }, 100);
        }
      }
    },
    keyFunction() {
      if (event.keyCode == 32) {
        this.Add();
        return false;
      }
    },
    Pass() {
      this.k++;
      console.log(1);
    },
    HLed(i) {
      if (this.k === 0) {
        return false;
      }
      var s = this.k % 14;
      if (i <= s + 2 && i >= s - 2) {
        return true;
      } else {
        return false;
      }
      // if (s < 5) {
      // } else if (s > 10) {
      // } else {
      //   return i - s < 5;
      // }
    },
    VLed(i) {
      if (this.k === 0) {
        return false;
      }
      var s = this.k % 69;
      if (i <= s + 2 && i >= s - 2) {
        return true;
      } else {
        return false;
      }
      // if (s < 5) {
      // } else if (s > 10) {
      // } else {
      //   return i - s < 5;
      // }
    }
    // play() {
    //   try {
    //     var audio = this.$refs.aud;
    //     console.log(audio);
    //     audio.cloneNode().play();
    //   } catch (ex) {
    //     alert(ex);
    //   }
    // },
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
}
.center {
  display: flex;
}
.bottom {
  display: flex;
  flex-direction: row-reverse;
}
.LVerticalLine {
  display: flex;
  flex-direction: column-reverse;
}
.VerticalLine {
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
  height: 30px;
  margin: 2px auto 2px;
  border-radius: 140px / 120px;
  display: flex;
  justify-content: center;
  align-content: center;
}
.Score {
  font-size: 22px;
  margin: auto;
}
.GetScore {
  background-color: rgb(250, 250, 250);
}
.GetPassScore {
  background-color: rgb(255, 89, 109);
}
</style>

