<template>
  <div class="uk-margin-small-top" v-if="totalPages != 1 && !loading">
    <nav>
      <ul class="uk-pagination">
        <li v-if="0 < (page-2)">
          <a tabindex="0" @click.prevent="loadPage(page-2)">
            <i class="uk-icon-angle-double-left"></i>
          </a>
        </li>
        <li v-if="0 < (page-1)">
          <a tabindex="0" @click.prevent="loadPage(page-1)">{{page - 1}}</a>
        </li>
        <li class="uk-active">
          <span tabindex="0">{{page}}</span>
        </li>
        <li v-if="totalPages >= (page+1)">
          <a tabindex="0" @click.prevent="loadPage(page+1)">{{page + 1}}</a>
        </li>
        <li v-if="page == 1 && totalPages >= (page+2)">
          <a tabindex="0" @click.prevent="loadPage(page+2)">{{page + 2}}</a>
        </li>
        <li v-if="page != 1 && totalPages >= (page+2)">
          <a tabindex="0" @click.prevent="loadPage(page+3)">
            <i class="uk-icon-angle-double-right"></i>
          </a>
        </li>
        <li v-if="page == 1 && totalPages >= (page+3)">
          <a tabindex="0" @click.prevent="loadPage(page+3)">
            <i class="uk-icon-angle-double-right"></i>
          </a>
        </li>
      </ul>
    </nav>
  </div>
</template>

<script>
export default {
  props: {
    page: Number,
    totalPages: Number,
    loading: Boolean,
    loadPage: Function
  }
};
</script>

<style lang="scss">
.uk-pagination {
  padding-top: 0px;
  padding-bottom: 0px;
}
</style>
