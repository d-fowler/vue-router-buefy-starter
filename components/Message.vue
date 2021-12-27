<template>
  <article class="message is-info" v-if="displayMessage">
    <div class="message-header">
      <p><slot name="title"></slot></p>
      <button class="delete" aria-label="delete" @click="$emit('close')"></button>
    </div>
    <div class="message-body">
      <slot></slot>
    </div>
  </article>
</template>

<script>
export default {
  props: ['displayMessage'],
  data() {
    return {
      
    }
  }
}
</script>

<style>
  .message {
    width: 600px;
    margin: auto;
  }
</style>
