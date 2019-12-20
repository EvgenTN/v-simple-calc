<template>
  <div class="app-div">
    <h2 class="app-header"> </h2>
    <div class="c-container">
      <div class="c-wrapper">
        <div class="c-table">
          <div class="c-wrap">
            <template v-if="exspression.length">
              <h2 class="c-display" :class="{ 'bigger': isMain }">{{ exspression }}</h2>
            </template>
            <h2 v-if="result === null" class="c-display">{{ screenValue }}</h2>
            <h2 v-else class="c-display" :class="{ 'bigger': !isMain }">{{ result }}</h2>
          </div>
        </div>
        <div class="c-button-wrap">
          <div class="c-btn" v-for="(n, i) in calcBtnList" :key="i">
            <button class="btn" :class="{ 'colored': n.color }" type="button"  @mouseup="doSmth(n)">{{ n.text }}</button>
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
      calcBtnList: [
        {
          text: "AC",
          color: 'orange',
          action: this.reset
        },
        {
          text: "<<",
          color: 'orange',
          action: this.clearLast
        },
        {
          text: "%",
          color: 'orange',
          action: this.getPercent
        },
        {
          text: "/",
          isString: true,
          color: 'orange',
          action: () => "/"
        },
        {
          text: "7",
          key: 7,
          isString: true,
          isNum: true,
          action: () => "7"
        },
        {
          text: "8",
          isString: true,
          isNum: true,
          action: () => "8"
        },
        {
          text: "9",
          isString: true,
          isNum: true,
          action: () => "9"
        },
        {
          text: "*",
          isString: true,
          color: 'orange',
          action: () => "*"
        },
        {
          text: "4",
          isString: true,
          isNum: true,
          action: () => "4"
        },
        {
          text: "5",
          isString: true,
          isNum: true,
          action: () => "5"
        },
        {
          text: "6",
          isString: true,
          isNum: true,
          action: () => "6"
        },
        {
          text: "-",
          isString: true,
          color: 'orange',
          action: () => "-"
        },
        {
          text: "1",
          isString: true,
          isNum: true,
          action: () => "1"
        },
        {
          text: "2",
          isString: true,
          isNum: true,
          action: () => "2"
        },
        {
          text: "3",
          isString: true,
          isNum: true,
          action: () => "3"
        },
        {
          text: "+",
          isString: true,
          color: 'orange',
          action: () => "+"
        },
        {
          text: "...",
          color: 'orange',
          action: () => {}
        },
        {
          text: "0",
          isString: true,
          isNum: true,
          action: () => "0"
        },
        {
          text: ".",
          isString: true,
          action: () => "."
        },
        {
          text: "=",
          isEq: true,
          color: 'orange',
          action: this.getResult
        }
      ],
      screenValue: '0',
      result: null,
      exspression: '',
      isMain: true
    };
  },
  methods: {
    defineKey(e) {
      this.calcBtnList.forEach(n => {
        if (n.text === e.key) this.doSmth(n);
      })
      if (e.key === 'Enter') {
        const l = this.exspression.slice(-1)
        if (l == '+' || l == '-' || l == '/' || l == '*') return;
        this.isMain = false
        this.exspression = this.getResult()
      }
      if (e.key === 'Backspace') {
        this.clearLast()
      }
      if (e.key === 'Delete') {
        this.reset()
      }
    },
    getPercent() {
      this.result /= 100
    },
    clearLast() {
      if (this.exspression.length) {
        this.exspression = this.exspression.slice(0, this.exspression.length - 1)
      }
    },
    reset() {
      this.screenValue = '0';
      this.exspression = '';
      this.result = null;
    },
    getResult() {
      if (this.exspression.length) {
        return new Function('return ' + this.exspression)()
      } else {
        alert('hernya')
      }
    },
    doSmth(n) {
      if (n.isEq) this.isMain = false
      if (n.isString) {
        this.isMain = true
        this.exspression += n.action()
        if (this.exspression.length && n.isNum) {
          this.result = this.getResult()
        }
      } else {
        n.action()
        if (n.text === '=') this.exspression = this.result
      }
    }
  },
  mounted() {
    window.addEventListener('keyup', event => {
      this.defineKey(event)
    })
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
  border-bottom: 1px solid lightgrey;
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
  color: rgb(122, 116, 116)
}
.c-button-wrap {
  display: flex;
  flex-wrap: wrap;
}
.c-btn {
  width: calc(25% - 2px);
  height: 50px;
  // border: 1px solid lightgrey;
}
.btn {
  width: 100%;
  height: 100%;
  cursor: pointer;
  // border: 4px solid darkblue;
  border: none;
  border-radius: 4px;
  background: white;
  color: darkblue;
  font-size: 22px;
  font-weight: 600;
  // overflow: hidden;
  // text-decoration: none;
  outline: none;
  &.colored {
    color: orangered;
  }
}
.bigger {
  font-size: 40px;
  color: black;
}
</style>