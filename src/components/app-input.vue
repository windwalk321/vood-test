<template>
  <div class="input-group col-md-4 col-sm-12">
    <div class="input-group-prepend">
      <span
        class="input-group-text bg-white"
        id="basic-addon1"
      >
        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-search" viewBox="0 0 16 16">
          <path d="M11.742 10.344a6.5 6.5 0 1 0-1.397 1.398h-.001c.03.04.062.078.098.115l3.85 3.85a1 1 0 0 0 1.415-1.414l-3.85-3.85a1.007 1.007 0 0 0-.115-.1zM12 6.5a5.5 5.5 0 1 1-11 0 5.5 5.5 0 0 1 11 0z"/>
        </svg>
      </span>
    </div>
    <input
      type="text"
      class="form-control"
      placeholder="Filter by author..."
      aria-label="Username"
      aria-describedby="basic-addon1"
      :value="value"
      @input="$emit('input', $event.target.value)"
    >
  </div>
</template>

<script>
export default {
  name: 'app-input',
  props: ['value']
}
</script>
