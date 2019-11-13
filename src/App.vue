<template>
  <div class="app-div">
    <h2 class="app-header">Welcome to awesome calc</h2>
    <div class="c-container">
      <div class="c-wrapper">
        <div class="c-table">
          <div class="c-wrap">
            <template v-if="operand.length">
              <h2 v-for="op in operand" :key="op" class="c-display">{{ op }}</h2>
            </template>
            <h2 class="c-display">{{ screenValue }}</h2>
          </div>
        </div>
        <div class="c-button-wrap">
          <div class="c-btn" v-for="(n, i) in calcBtnList" :key="i">
            <button class="btn" @click="doSmth(n.action, n.isNum, n.isOperator)">{{ n.text }}</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      screenValue: 0,
      result: null,
      operand: [],
      calcBtnList: [
        {
          text: "AC",
          action: this.reset
        },
        {
          text: "<<",
          action: () => {}
        },
        {
          text: "%",
          action: () => {}
        },
        {
          text: "/",
          isOperator: true,
          action: () => "/"
        },
        {
          text: "7",
          isNum: true,
          action: () => "7"
        },
        {
          text: "8",
          isNum: true,
          action: () => "8"
        },
        {
          text: "9",
          isNum: true,
          action: () => "9"
        },
        {
          text: "x",
          isOperator: true,
          action: () => "x"
        },
        {
          text: "4",
          isNum: true,
          action: () => "4"
        },
        {
          text: "5",
          isNum: true,
          action: () => "5"
        },
        {
          text: "6",
          isNum: true,
          action: () => "6"
        },
        {
          text: "-",
          isOperator: true,
          action: () => "-"
        },
        {
          text: "1",
          isNum: true,
          action: () => "1"
        },
        {
          text: "2",
          isNum: true,
          action: () => "2"
        },
        {
          text: "3",
          isNum: true,
          action: () => "3"
        },
        {
          text: "+",
          isOperator: true,
          action: () => "+"
        },
        {
          text: "...",
          action: () => {}
        },
        {
          text: "0",
          isNum: true,
          action: () => "0"
        },
        {
          text: ".",
          isNum: true,
          action: () => "."
        },
        {
          text: "=",
          action: this.getResult
        }
      ]
    };
  },
  methods: {
    reset() {
      this.screenValue = 0;
      this.operand = [];
      this.result = null;
    },
    getResult() {
      const op = [...this.operand]
      for (let i = 0; i < op.length; i++) {
        let n = Number(op[i])
        console.log('n', n)
      }
      console.log("resSplit", this.result.split());
      console.log("resNum", Number(this.result));
      console.log("res", this.result);
    },
    doSmth(action, isNum, isOperator) {
      if (isNum) {
        if (this.screenValue == 0) {
          this.screenValue = action();
          console.log("res1", this.result);
          this.result = action();
          console.log("res1", this.result);
        } else {
          this.screenValue += action();
          console.log("res2", this.result);
          this.result += action();
          // this.result ? this.result += this.screenValue : this.result = this.screenValue
          console.log("res2", this.result);
        }
      } else if (isOperator) {
        this.operand.push(this.screenValue);
        this.result += action();
        this.screenValue = action() + " ";
      } else {
        action();
      }
    }
  }
};
</script>

<style lang="scss">
body {
  font-family: Arial, Helvetica, sans-serif;
}
.app-div {
  width: 100%;
  height: 100%;
  padding: 20px;
}
.app-header {
  text-align: center;
}
.c-container {
  display: flex;
  justify-content: center;
  align-items: center;
}
.c-wrapper {
  width: 100%;
  max-width: 400px;
  height: 100%;
  border: 2px solid grey;
  border-radius: 4px;
}
.c-table {
  width: 100%;
  height: 200px;
  border-bottom: 1px solid grey;
  display: flex;
  justify-content: flex-end;
  align-items: flex-end;
}
.c-wrap {
  text-align: right;
  padding: 15px;
}
.c-display {
  margin: 0;
}
.c-button-wrap {
  display: flex;
  flex-wrap: wrap;
}
.c-btn {
  width: calc(25% - 2px);
  height: 50px;
  border: 1px solid lightgrey;
}
.btn {
  width: 100%;
  height: 100%;
  cursor: pointer;
}
</style>