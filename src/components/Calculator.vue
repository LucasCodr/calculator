<template>
  <div class="calculator">
    <input class="display" v-model="current">
    <span class="btn" @click="clearDisplay">C</span>
    <span class="btn" @click="sign">+/-</span>
    <span class="btn" @click="percent">%</span>
    <span class="btn operator" @click="divide">&#247;</span>
    <span class="btn" @click="append(7)">7</span>
    <span class="btn" @click="append(8)">8</span>
    <span class="btn" @click="append(9)">9</span>
    <span class="btn operator" @click="times">X</span>
    <span class="btn" @click="append(4)">4</span>
    <span class="btn" @click="append(5)">5</span>
    <span class="btn" @click="append(6)">6</span>
    <span class="btn operator" @click="minus">-</span>
    <span class="btn" @click="append(1)">1</span>
    <span class="btn" @click="append(2)">2</span>
    <span class="btn" @click="append(3)">3</span>
    <span class="btn operator" @click="add">+</span>
    <span class="zero btn" @click="append(0)">0</span>
    <span class="btn" @click="dot">.</span>
    <span class="btn operator" @click="equal">=</span>
  </div>
</template>

<script>
export default {
  data() {
    return {
      current: "0",
      operator: null,
      previous: null,
      operatorClicked: false
    };
  },
  methods: {
    clearDisplay() {
      this.current = "";
    },
    sign() {
      this.current =
        this.current.charAt(0) === "-"
          ? this.current.slice(1)
          : `-${this.current}`;
    },
    percent() {
      this.current = `${parseFloat(this.current / 100)}`;
    },
    append(number) {
      if(this.operatorClicked) {
        this.current = '';
        this.operatorClicked = false;
      }
      this.current += number;
    },
    dot() {
      if (this.current.indexOf(".") !== -1) return;
      this.append(".");
    },
    setPrevious() {
      this.previous = this.current;
      this.operatorClicked = true;
    },
    divide() {
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },
    add() {
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    minus() {
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },
    times() {
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    equal() {
      this.current = `${this.operator(parseFloat(this.previous), parseFloat(this.current))}`
      this.previous = null;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calculator {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  font-size: 60px;
  width: 400px;
  margin: 0 auto;
}

.display {
  grid-column: 1 / 5;
  background-color: #333;
  color: #fff;
  font-size: 60px;
  border: none;
  outline: none;
  padding: 10px;
}

.zero {
  grid-column: 1 / 3;
}

.btn {
  border: 1px solid #999;
  background-color: #eee;
}

.btn:hover {
  cursor: pointer;
}

.btn:active {
  background-color: #333;
}

.operator {
  background-color: orange;
  color: #fff;
}
</style>
