<template>
  <div class="OuterFrame">
    <div v-for="i in 20" :key="i" class="ScoreBox">
      <span class="Score">{{i}}</span>
    </div>
  </div>
</template>

<script>
export default {
  props: ["msg"]
};
</script>
<style lang="scss" scoped>
.OuterFrame {
  background-color: rgba(146, 134, 101, 0.8);
  width: 150px;
  height: 880px;
  display: flex;
  flex-direction: column-reverse;
  align-content: center;
  padding-top: 3px;
  padding-bottom: 3px;
  font-family: "Microsoft JhengHei";
}
.ScoreBox {
  background-color: rgba(132, 132, 142, 0.8);
  width: 135px;
  height: 40px;
  margin: 2px auto 2px;
  border-radius: 140px / 120px;
  display: flex;
  justify-content: center;
  align-content: center;
  // margin-left: auto;
  // margin-right: auto;
}
.Score {
  font-size: 30px;
  margin: auto;
}
.GetScore {
  background-color: rgba(255, 255, 255, 0.8);
}
</style>

