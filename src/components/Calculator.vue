<template>
  <div class="calculator">
    <Display :value="displayValue" />
    <Buttons @buttonClick="handleButtonClick" />
  </div>
</template>

<script>
import Display from "./Display.vue";
import Buttons from "./Buttons.vue";

export default {
  components: {
      Buttons,
      Display,
    },
  data() {
    return {
      displayValue: "0",
      operator: null,
      waitingForOperand: false,
      operand: null,
      memoryValue: null,
    };
  },
  methods: {
    handleButtonClick(buttonValue) {
      if (buttonValue === ".") {
        // Only allow one decimal point (note to self - -1 is the result of a false reading (doesnt contain))
        if (this.displayValue.indexOf(".") === -1) {
          this.displayValue += ".";
        }
      } else if (!isNaN(buttonValue)) {
        if (this.waitingForOperand) {
          this.displayValue = buttonValue;
          this.waitingForOperand = false;
        } else {
          this.displayValue =
            this.displayValue === "0"
              ? buttonValue
              : this.displayValue + buttonValue;
        }
      } else {
        switch (buttonValue) {
          case "+":
          case "-":
          case "*":
          case "/":
            this.handleOperator(buttonValue);
            break;
          case "=":
            this.handleEqual();
            break;
          case "+/-":
            this.handleSign();
            break;
          case "%":
            this.handlePercent();
            break;
          case "√":
            this.handleSqrt();
            break;
          case "MS":
            this.handleMemoryStore();
            break;
          case "MR":
            this.handleMemoryRecall();
            break;
          case "MC":
            this.handleMemoryClear();
            break;
          case "M+":
            this.handleMemoryAdd();
            break;
          case "M-":
            this.handleMemorySubtract();
            break;
          case "AC":
            this.handleClear();
            break;
          case "C":
            this.handleDisplayClear();
            break;
        }
      }
    },
    handleOperator(newOperator) {
      if (this.operator === null) {
        this.operator = newOperator;
        this.operand = parseFloat(this.displayValue);
        this.displayValue = "0";
      } else {
        const currentValue = parseFloat(this.displayValue);
        const newValue =
          this.operator === "+"
            ? this.operand + currentValue
            : this.operator === "-"
            ? this.operand - currentValue
            : this.operator === "*"
            ? this.operand * currentValue
            : this.operand / currentValue;
        this.operator = newOperator;
        this.operand = newValue;
        this.displayValue = String(newValue);
      }
      this.waitingForOperand = true;
    },

    handleEqual() {
      if (this.operator !== null) {
        const currentValue = parseFloat(this.displayValue);
        const newValue =
          this.operator === "+"
            ? this.operand + currentValue
            : this.operator === "-"
            ? this.operand - currentValue
            : this.operator === "*"
            ? this.operand * currentValue
            : this.operand / currentValue;
        this.operator = null;
        this.operand = null;
        this.displayValue = String(newValue);
        this.waitingForOperand = true;
      }
    },

    handleSign() {
      this.displayValue = String(parseFloat(this.displayValue) * -1);
    },

    handlePercent() {
      this.displayValue = String(parseFloat(this.displayValue) / 100);
    },
    
    handleSqrt() {
      this.displayValue = String(Math.sqrt(parseFloat(this.displayValue)));
    },

    handleMemoryStore() {
      this.memoryValue =parseFloat(this.displayValue);
      this.displayValue = "0";
    },

handleMemoryRecall() {
    if (this.memoryValue !== null) {
    this.displayValue = String(this.memoryValue);
    }
},

handleMemoryAdd() {
    if (this.memoryValue !== null) {
    this.memoryValue += parseFloat(this.displayValue);
    }
    this.displayValue = "0";
},

handleMemorySubtract() {
    if (this.memoryValue !== null) {
    this.memoryValue -= parseFloat(this.displayValue);
    }
    this.displayValue = "0";
},

handleMemoryClear() {
    this.memoryValue = null;
 },

handleClear() {
    this.displayValue = "0";
    this.operator = null;
    this.waitingForOperand = false;
    this.operand = null;
    this.memoryValue = null;
 },

  handleDisplayClear() {
      this.displayValue = "0";
    },
  },
  
};
</script>
<style>
.calculator {
  background-color: #b81818;
  border-radius: 5px;
  padding: 16px;
}

.display {
  font-size: 32px;
  line-height: 1.5;
  padding: 8px;
  margin-bottom: 16px;
  background-color: #fff;
  border-radius: 3px;
  text-align: right;
}

.keys {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-gap: 12px;
}

button {
  font-size: 24px;
  padding: 16px;
  border-radius: 3px;
  border: 1px solid #ccc;
  box-shadow: 0 2px 2px rgba(0, 0, 0, 0.05);
  background-color: #f9f9f9;
  color: #333;
  cursor: pointer;
}

</style>