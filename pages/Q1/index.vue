<template>
  <div class="container">
    <div id="col-1">
      <input
        v-model="numberInput"
        v-on:change="round"
        type="number"
        placeholder="กรุณาใส่ตัวเลข"
      />
    </div>
    <div id="col-2">
      <select v-model="selectedFunc">
        <option disabled value="">กรุณาเลือกฟังชั่น</option>
        <option>isPrime</option>
        <option>isFibonacci</option>
      </select>
    </div>
    <div id="col-3">
      <div v-html="result" />
    </div>
  </div>
</template>
<script>
export default {
  name: "MainPage",
  data() {
    return {
      numberInput: null,
      selectedFunc: "",
      loading: false,
      fiboList: [1, 1],
    };
  },
  methods: {
    round(e) {
      const value = e.target.value;
      if (value >= 1 && !Number.isInteger(value)) {
        this.numberInput = Math.round(value);
      } else {
        this.numberInput = 1;
      }
    },

    isPrime(num) {
      for (var i = 2; i < num; i++)
        if (num % i === 0) {
          return false;
        }
      return num > 1;
    },

    isPerfectSquare(x) {
      var s = Math.sqrt(x);
      return s * s == x;
    },

    isFibanacci(n) {
      return (
        this.isPerfectSquare(5 * n * n + 4) || isPerfectSquare(5 * n * n - 4)
      );
    },

    getResult() {
      const { numberInput } = this;
      if (Number.isInteger(numberInput) && numberInput > 0) {
        let answer;
        if (this.selectedFunc === "isPrime") {
          answer = this.isPrime(numberInput);
        }
        if (this.selectedFunc === "isFibonacci") {
          answer = this.isFibanacci(numberInput);
        }
        return answer;
      }
      return "";
    },
  },
  computed: {
    result() {
      return this.getResult();
    },
  },
};
</script>

<style scoped>
.container {
  display: flex;
  min-width: 600px;
  width: 100%;
}

#col-1 {
  width: 200px;
}

#col-2 {
  flex: 1;
  min-width: 100px;
}

#col-3 {
  width: 300px;
}

#col-1,
#col-2,
#col-3 {
  height: 100vh;
  border: 1px solid black;
  padding: 5px;
}
</style>
