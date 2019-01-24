<template>
  <div class="integration-item" v-bind:class="{ 'integration-item--selected': selected }">
    <div class="integration-item__left">
      <img :src=item.image_url class="integration-item__image">
    </div>
    <div class="integration-item__right">
      <div class="uk-form-text-label">{{item.title}}</div>
      <div class="uk-text-muted">{{truncate(item.description)}}</div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    current: Object,
    item: Object
  },
  computed: {
    selected() {
      if (typeof this.current === 'undefined'||this.current == null) return false
      return this.current.id == this.item.id
    }
  },
  methods: {
    truncate(string) {
      let maxLength = 50
      if(string.length <= maxLength) {
        return string
      }

      let trimmed = string.substring(0, Math.min(maxLength, string.length))
      trimmed = trimmed.substr(0, Math.min(trimmed.length, trimmed.lastIndexOf(' ')))
      return `${trimmed}...`
    }
  }
}
</script>

<style lang="scss"> 
.integration-item {
  border: 1px solid #ddd;
  padding: 10px;
  background: #fff;
  display: flex;
  justify-content: space-between;

  &.integration-item--selected {
    border-color: #09b3af;
    outline: 0;
    background: #f2f9f8;
    color: #444;
  }
}
.integration-item__left {
  width: 60px;
  height: 60px;
  min-height: 60px;
  flex-shrink: 0;
  overflow: hidden;
  border: 1px solid #ddd;
  background: #eee;
}
.integration-item__image {
  display: block;
  height: 60px;
  max-width: 60px;
  max-height: 60px;
  margin: 0 auto;
}
.integration-item__right {
  flex-grow: 1;
  padding-left: 10px;
  word-wrap: break-word;
}
</style>
