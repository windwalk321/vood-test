<template>
  <div class="card">
    <div class="card-body">
      <h5 class="card-title text-primary">{{post.title}}</h5>
      <p class="card-text">{{post.body}}</p>
      <small class="text-muted">{{post.author.name}}</small>
    </div>
  </div>
</template>

<script>
export default {
  name: 'app-posts-item',
  props: {
    post: {
      type: Object,
      default: () => {}
    }
  }
}
</script>
