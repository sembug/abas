<template>
  <div>
    <h1>Other</h1>
    <p>Lorem ipsum dolor sit, amet consectetur adipisicing elit. Ratione magnam nam, neque accusantium blanditiis eum possimus facere? Nobis asperiores, quam rem doloribus eligendi iure dolorum, quis itaque quidem vitae beatae!</p>
    <span>Message is: {{ message }}</span>
    <br>
    <input type="text" v-model="message" placeholder="edit me">
  </div>
</template>

<script>
export default {
  name: 'OtherPage',
  data () {
    return {
      message: ''
    }
  }
}
</script>

<style>
</style>
