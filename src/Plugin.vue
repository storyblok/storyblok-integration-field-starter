<template>
  <div class="integration">
    
    <div v-if="!modalIsOpen">
      <IntegrationItem v-if="model.item" :item=model.item></IntegrationItem>
      <button class="uk-button uk-width-1-1 uk-margin-small-top" @click.prevent=openSelection>Open Selection</button>
    </div>

    <div class="uk-form" v-if="modalIsOpen">
      <IntegrationSelection :options=options :select=selectItem :current=model.item :close=closeSelection></IntegrationSelection>      
    </div>

  </div>
</template>

<script>
import IntegrationItem from './IntegrationItem'
import IntegrationSelection from './IntegrationSelection'

export default {
  mixins: [window.Storyblok.plugin],
  data() {
    return {
      modalIsOpen: false,
    }
  },
  methods: {
    initWith() {
      return {
        // needs to be equal to your storyblok plugin name
        plugin: 'integration-field',
        item: null
      }
    },
    pluginCreated() {
      this.checkOptions()
    },
    openSelection() {
      this.modalIsOpen = true
      this.$emit('toggle-modal', true)
    },
    closeSelection() {
      this.modalIsOpen = false
      this.$emit('toggle-modal', false)
    },
    selectItem(item) {
      this.model.item = item
    },
    checkOptions() {
      if (typeof this.options.endpoint === 'undefined') {
        // eslint-disable-next-line
        console.error(`Please provide the option 'endpoint' with your endpoint url as value`)
      }
      if (typeof this.options.token === 'undefined') {
        // eslint-disable-next-line
        console.info(`If you need an authentication using Basic Auth add a option with the name token.`)
        // eslint-disable-next-line
        console.info(`Your provided token will be used as username performing a Basic Auth, the password will be left blank`)
      }
    }
  },
  components: {
    IntegrationItem,
    IntegrationSelection
  },
  watch: {
    'model': {
      handler(value) {
        this.$emit('changed-model', value);
      },
      deep: true
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
