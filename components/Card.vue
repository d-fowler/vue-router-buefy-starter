<template>
  <div class="card">
    <div class="card-image">
      <figure class="image is-3by3">
        <img src="https://drive.google.com/uc?export=view&id=1AXPvDqCmSDtglsEy73kdahGjokCZjXIW" alt="Placeholder image">
      </figure>
    </div>
    <div class="card-content">
      <div class="media">
        <div class="media-left">
          <figure class="image is-48x48">
            <img src="https://drive.google.com/uc?export=view&id=1uZBhjDzzecLRCR-b4D6nNVWGORzz9-Sk" alt="Placeholder image">
          </figure>
        </div>
        <div class="media-content">
          <p class="title is-4"><slot name="name"></slot></p>
          <p class="subtitle is-6"><slot name="handle"></slot></p>
        </div>
      </div>

      <div class="content">
        <slot></slot>
        <br>
        <time datetime="2017-12-14">10:12 PM - 12 Dec 2017</time>
      </div>
    </div>
  </div>
</template>

<script>
export default {

}
</script>

<style scope>
  .card {
    width: 400px;
    margin: auto;
  }
  .content {
    text-align: left;
  }
  time {
    display: block;
    text-align: right;
    font-size: .8rem;
  }
</style>
