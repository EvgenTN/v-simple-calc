<template>
  <div class="app-div">
    <h2 class="app-header">Welcome to awesome calc</h2>
    <div class="c-container">
      <div class="c-wrapper">
        <div class="c-table">
          <h2 class="c-display">{{ result }}</h2>
        </div>
        <div class="c-button-wrap">
          <div class="c-btn" v-for="(n, i) in calcBtnList" :key="i">
            <button class="btn" @click="doSmth(n.action)">{{ n.text }}</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      result: 0,
      calcBtnList: [
        {
          text: 'AC',
          action: this.reset
        },
        {
          text: '<<',
          action: () => {}
        },
        {
          text: '%',
          action: () => {}
        },
        {
          text: '/',
          action: () => {}
        },
        {
          text: '7',
          action: () => 7
        },
        {
          text: '8',
          action: () => 8
        },
        {
          text: '9',
          action: () => 9
        },
        {
          text: 'x',
          action: () => {}
        },
        {
          text: '4',
          action: () => 4
        },
        {
          text: '5',
          action: () => 5
        },
        {
          text: '6',
          action: () => 6
        },
        {
          text: '-',
          action: () => {}
        },
        {
          text: '1',
          action: () => 1
        },
        {
          text: '2',
          action: () => 2
        },
        {
          text: '3',
          action: () => 3
        },
        {
          text: '+',
          action: () => {}
        },
        {
          text: '...',
          action: () => {}
        },
        {
          text: '0',
          action: () => 0
        },
        {
          text: '.',
          action: () => {}
        },
        {
          text: '=',
          action: () => {}
        }
      ]
    }
  },
  methods: {
    reset() {
      this.result = 0
    },
    doSmth(action) {
      this.result = action()
    }
  }
}
</script>

<style lang="scss">
body {
  font-family: Arial, Helvetica, sans-serif;
}
.app-div {
  width: 100%;
  height: 100%;
  // display: flex;
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
.c-display {
  margin: 0;
  padding: 15px;
}
.c-button-wrap {
  display: flex;
  flex-wrap: wrap;
  // height: 250px;
}
.c-btn {
  width: calc(25% - 2px);
  height: 50px;
  border: 1px solid lightgrey;
}
.btn {
  width: 100%;
  height: 100%;
}
</style>