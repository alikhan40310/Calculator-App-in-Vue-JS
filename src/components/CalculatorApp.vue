
<style> 

.items {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  width: 100%;
  padding-bottom: 12%;
}
.content {
  background: #234;
  width: 25vw;
  border-radius: 30px;
  text-align: right;
  font-weight: bold;
  font-size: 30px;
  height: 100%;
  box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.5);
  margin-top: 8rem;
  padding-bottom: 20%;
  word-wrap: break-word;
}
.main-bg {
  background: transparent;
  padding: 10px;
  border-radius: 5px;
  font-weight: bold;
  color: var(--inside-color);
  font-size: 50px;
  margin-bottom: 10px;
}
.bg-vue-dark{
    background: #223341;
    box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.2);
}
.hover-class{transition: all .5s ease;}
.hover-class:hover{
    cursor: pointer;
    background: var(--hover-color);
    transition: all 0.5s ease;
    color: var(--hover-text-color);
}
.fonts{
    font-weight: 600;
    border-radius: 25px;
    color: var(--text-color);
} 
.text-orange{
    /* background: #3fb984; */
    color: var(--text-orange);
}
.bg-vue-dark{
  background: var(--btn-color);
}
.bg-vue-orange{
  background-color: #f88238;
  color: #fff;
  border-radius: 10px;
}
@media (max-width: 1300px) {
  .content{
    width:auto;
  }
}
@media screen and (max-width:600px){
  .content{
    width:80%;
    font-size: 10px;
  }
  .main-bg{font-size: 40px;}
}

@media screen and (max-width:479px){
  .content{
    width: 100%;
  }
  .main-bg{font-size: 35px;}
}
</style>


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
          // when user enter the value, the length of the value is less then 12
                   
 
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
          <div class="col-3" :class="{'col-6 ': ['='].includes(n)}" v-for="n in calculatorElement" :key="n">    
            <div class="fonts lead text-center m-1 py-4 bg-vue-dark  hover-class"  
            :class="{'text-orange ': ['C','√', '*','/','-','+','%', '='].includes(n)},[ {'bg-vue-orange themecolor': ['='].includes(n)}]"
            @click="action(n)">
                {{ n }}
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

