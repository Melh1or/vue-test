<template>
  <div>
    <mcv-loading v-if='isLoading' />
    <mcv-error-message v-if='error' />

    <div class='sidebar' v-if='popularTags'>
      <p>Popular tags</p>
      <div class='tag-list'>
        <router-link
          v-for='(popularTag) in popularTags'
          :key='popularTag'
          :to='{name: "tags", params: {slug: popularTag}}'
          class='tag-default tag-pill ng-binding ng-scope'
        >
          {{ popularTag }}
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
import {mapState} from 'vuex'
import {actionTypes} from '@/store/modules/popularTags'
import McvLoading from '@/components/Loading'
import McvErrorMessage from '@/components/ErrorMessage'

export default {
  name: 'McvPopularTags',
  components: {
    McvLoading,
    McvErrorMessage
  },
  mounted() {
    this.$store.dispatch(actionTypes.getTags)
  },
  computed: {
    ...mapState({
      isLoading: state => state.popularTags.isLoading,
      popularTags: state => state.popularTags.data,
      error: state => state.popularTags.error
    }),
    url() {
      return this.$route.path
    }
  }
}
</script>
