<template>
  <div>
    <h1>Dashboard</h1>
    <p><a href="#" @click.prevent="addTab({ name: 'Another', componentName: 'AnotherPage'})">Another Page</a></p>
    <p><a href="#" @click.prevent="addTab({ name: 'Other', componentName: 'OtherPage'})">Other Page</a></p>
  </div>
</template>

<script>
import bus from '../bus.js';
export default {
  name: 'HomePage',
  data () {
    return {
      message: ''
    }
  },
  methods: {
    addTab: function (tab)  {
      bus.$emit('addTab', tab);
    }
  }
}
</script>

<style>
</style>
