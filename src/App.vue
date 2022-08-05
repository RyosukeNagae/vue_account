<template>
  <h1>入力画面</h1>
  <div>
    <input type="number" v-model="inputValue" />
    <div>入力額: {{ inputValue }} 円</div>
    <button v-on:click="deposit">入金</button>
    <button v-on:click="withdraw" v-bind:disabled="disabled">出金</button>
  </div>

  <h1>口座残高</h1>
  <div>
    <div>残高: {{ balance }} 円</div>
  </div>

  <h1>取引記録</h1>
  <div v-for="log in logs" :key="log.date">
    日付: {{ log.date }}<br />操作: {{ log.type }}<br />金額: {{ log.money }}
  </div>
</template>

<script>
export default {
  data() {
    return {
      inputValue: 0,
      balance: 0,

      logs: [],
    };
  },

  methods: {
    // 入金
    deposit() {
      this.logs.push({
        date: new Date(),
        type: "入金",
        money: this.inputValue,
      });

      this.balance += Number(this.inputValue);
      this.inputValue = 0;
    },

    // 出金
    withdraw() {
      this.logs.push({
        date: new Date(),
        type: "出金",
        money: this.inputValue,
      });

      if (this.balance >= this.inputValue) {
        this.balance -= this.inputValue;
        this.inputValue = 0;
      }
    },
  },

  computed: {
    disabled() {
      if (this.balance >= this.inputValue) {
        return false;
      }
      return true;
    },
  },
};
</script>
