<template>
  <div class="calculator__container">
    <div class="calculator__button calculator__display">{{current || '0'}}</div>
    <div @click="clear" class="calculator__button sub__operator">AC</div>
    <div @click="sign" class="calculator__button sub__operator">&#43;/&#8722;</div><!--(+/-)-->
    <div @click="percent" class="calculator__button sub__operator">&#37;</div><!--(%)-->
    <div @click="divide" class="calculator__button operator">&#247;</div><!--(÷)-->
    <div @click="append('7')" class="calculator__button">7</div>
    <div @click="append('8')" class="calculator__button">8</div>
    <div @click="append('9')" class="calculator__button">9</div>
    <div @click="times" class="calculator__button operator">&#215;</div><!--(×)-->
    <div @click="append('4')" class="calculator__button">4</div>
    <div @click="append('5')" class="calculator__button">5</div>
    <div @click="append('6')" class="calculator__button">6</div>
    <div @click="minus" class="calculator__button operator">&#8722;</div><!--(-)-->
    <div @click="append('1')" class="calculator__button">1</div>
    <div @click="append('2')" class="calculator__button">2</div>
    <div @click="append('3')" class="calculator__button">3</div>
    <div @click="add" class="calculator__button operator">&#43;</div><!--(+)-->
    <div @click="append('0')" class="calculator__button zero">0</div>
    <div @click="dot" class="calculator__button">.</div>
    <div @click="equal" class="calculator__button operator">&#61;</div><!--(=)-->

  </div>
</template>

<script>
export default {
  data() {
    return {
      previous: null,
      current: '',
      operator: null,
      operatorClicked: false,
    }
  },
  methods: {
    /*This method clears out the display div*/
    clear() {
      this.current = '';
    },
    /*This method adds/subtracts a negative character at index 0*/
    sign() {
      this.current = this.current.charAt(0) === '-' ?
        this.current.slice(1) : `-${this.current}`;
    },
    /*This method takes the displayed integer and divides it by 100*/
    percent() {
      this.current = `${parseFloat(this.current) / 100}`
    },
    /*This method joins two string together over and over*/
    append(number) {
      if (this.operatorClicked) {
        this.current = '';
        this.operatorClicked = false;
      }
      this.current = `${this.current}${number}`;
    },
    /*This method appends a '.' one time*/
    dot() {
      if (this.current.indexOf('.') === -1) {
        this.append('.');
      }
    },
    setPrevious() {
      this.previous = this.current;
      this.operatorClicked = true;
    },
    divide() {
      this.operator = (a, b) => b / a;
      this.setPrevious();
    },
    times() {
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    minus() {
      this.operator = (a, b) => b - a;
      this.setPrevious();
    },
    add() {
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    equal() {
      this.current = `${this.operator(
        parseFloat(this.current),
        parseFloat(this.previous)
      )}`;
      this.previous = null;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only
<style scoped></style>-->
