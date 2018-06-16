<template>
  <div :id="todo.id" v-bind:class="{active: todo.is_active}">
    <p>{{ todo.name }}</p>
    <p class="todo_elapsed_time">{{ this.h + ':' + this.m + ':' + this.s  }}</p>
    <button v-on:click="start()">開始</button>
    <button v-on:click="stop()">中断</button>
    <button v-on:click="done()">完了</button>
  </div>
</template>

<script>
  export default {
    name: 'todo',
    props: [
      'todo'
    ],
    data: function () {
      return {
        todo: this.todo,
        interval_id: null,
        h: '00',
        m: '00',
        s: '00'
      }
    },
    methods: {
      start () {
        var _this = this
        this.interval_id = setInterval(function () {
          var elapsedTime = _this.todo.elapsed_time++

          _this.h = _this.get_hour_str(elapsedTime)
          _this.m = _this.get_min_str(elapsedTime)
          _this.s = _this.get_sec_str(elapsedTime)
        }, 1000)
      },
      stop () {
        clearInterval(this.interval_id)
      },
      done () {
        this.$emit('done')
      },
      get_hour_str (time) {
        var h = time / 3600 | 0
        return h < 10 ? '0' + h : h
      },
      get_min_str (time) {
        var min = time % 3600 / 60 | 0
        return min < 10 ? '0' + min : min
      },
      get_sec_str (time) {
        var sec = time % 60
        return sec < 10 ? '0' + sec : sec
      }
    }
  }
</script>

<style>
</style>
