
<script>
export default {
  name: "Calculator",
  data() {
    return {
      calculatorValue: "",
      calculatorElement: [
        "C",
        "*",
        "/",
        "-",
        7,
        8,
        9,
        "+",
        4,
        5,
        6,
        "%",
        1,
        2,
        3,
        '√',
        0,
        ".",
        "="
      ],
      operator:null,
      previousCalculatorValue: '',
    };
  },
  methods: {
      action(n) {
        //   append value
          if (!isNaN(n) || n === ".") {
              this.calculatorValue +=n + '';
          }
        //   clear value
        if (n === "C") {
            this.calculatorValue = "";
        }
        // percentage value
        if (n === "%") {
            this.calculatorValue = this.calculatorValue / 100;
        }
        
        if(['/','*','-','+','√'].includes(n)){
            this.operator = n;
            this.previousCalculatorValue = this.calculatorValue;
            this.calculatorValue = '';
            // square root
            if(n === '√'){
                this.calculatorValue = Math.sqrt(this.previousCalculatorValue);
            }


        }
        // calculate value
        if (n === "=") {
            this.calculatorValue = eval(this.previousCalculatorValue + this.operator + this.calculatorValue);

            this.previousCalculatorValue = '';
            this.operator = null;
        }

      },
  }
};
</script>

<template>
  <div class="container">
    <div class="items">
      <div class="content p-3">
        <div class="main-bg">
          {{ calculatorValue || 0 }}
        </div>
        <div class="d-flex flex-wrap mt-4">
          <div class="col-3 " :class="{'col-6': ['='].includes(n)}" v-for="n in calculatorElement" :key="n">    
            <div class="fonts lead text-white text-center m-1 py-3 bg-vue-dark rounded hover-class" 
            :class="{'bg-vue-green': ['C','√', '*','/','-','+','%', '='].includes(n)}"
            @click="action(n)">
                {{ n }}
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>

.items {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  width: 100%;

}
.content {
  background: #234;
  width: auto;
  border-radius: 5px;
  margin-top: 10rem;
  text-align: right;
  font-weight: bold;
  font-size: 30px;
  height: 100%;
  box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.5);
}
.main-bg {
  background: #31475e;
  padding: 10px;
  border-radius: 5px;
  font-weight: bold;
}
.bg-vue-dark{
    background: #31475e;
}
.hover-class:hover{
    cursor: pointer;
    background: #3d5875;
}
.bg-vue-green{
    background: #3fb984;
}
.fonts{
    font-size: 22px;
    font-weight: 600;
}
</style>
