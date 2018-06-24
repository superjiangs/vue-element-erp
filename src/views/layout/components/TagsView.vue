<template>
  <scroll-pane class='tags-view-container' ref='scrollPane'>
    <router-link ref='tag' class="tags-view-item" :class="isActive(tag)?'active':''" v-for="tag,index in Array.from(visitedViews)" :to="tag.path":key="tag.path">
      {{generateTitle(tag.title)}}
      <span v-if="index != 0" class='el-icon-close' @click='closeViewTags(tag,$event)'></span>
    </router-link>
  </scroll-pane>
</template>

<script>
import ScrollPane from '@/components/ScrollPane'
import { generateTitle } from '@/utils/i18n'

export default {
  components: { ScrollPane },
  computed: {
    visitedViews() {
      return this.$store.state.app.visitedViews
    }
  },
  mounted() {
    this.addViewTags()
  },
  methods: {
    generateTitle,
    closeViewTags(view, $event) {
      this.$store.dispatch('delVisitedViews', view).then((views) => {
        if (this.isActive(view)) {
          const latestView = views.slice(-1)[0]
          if (latestView) {
            this.$router.push(latestView.path)
          } else {
            this.$router.push('/')
          }
        }
      })
      $event.preventDefault()
    },
    generateRoute() {
      if (this.$route.name) {
        return this.$route
      }
      return false
    },
    addViewTags() {
      const route = this.generateRoute()
      if (!route) {
        return false
      }
      this.$store.dispatch('addVisitedViews', route)
    },
    isActive(route) {
      return route.path === this.$route.path || route.name === this.$route.name
    },
    moveToCurrentTag() {
      const tags = this.$refs.tag
      this.$nextTick(() => {
        for (const tag of tags) {
          console.log(tag.to)
          if (tag.to === this.$route.path) {
            alert(1)
            this.$refs.scrollPane.moveToTarget(tag.$el)
            break
          }
        }
      })
    }
  },
  watch: {
    $route() {
      this.addViewTags()
      this.moveToCurrentTag()
    }
  }
}
</script>

<style rel="stylesheet/scss" lang="scss" scoped>
.tags-view-container {
  background: #6ec4ff;
  height: 40px;
  border-bottom: 1px solid #d8dce5;
  box-shadow: 0 1px 3px 0 rgba(0, 0, 0, .12), 0 0 3px 0 rgba(0, 0, 0, .04);
  .tags-view-item {
    display: inline-block;
    position: relative;
    height: 40px;
    line-height: 40px;
    /*border: 1px solid #d8dce5;*/
    color: #fff;
    background: #6ec4ff;
    padding: 0 8px;
    font-size: 12px;
    margin-left: 5px;
    /*margin-top: 4px;*/
    text-align: center;
    &:first-of-type {
      margin-left: 15px;
    }
    &.active {
      background-color: #fff;
      color: #000;
      /*border-color: orange;*/
      &::before {
        content: '';
        background: #fff;
        display: inline-block;
        width: 8px;
        height: 8px;
        border-radius: 50%;
        position: relative;
        margin-right: 2px;
      }
    }
  }
}
</style>

<style rel="stylesheet/scss" lang="scss">
.tags-view-container {
  .tags-view-item {
    .el-icon-close {
      width: 16px;
      height: 16px;
      vertical-align: 2px;
      border-radius: 50%;
      text-align: center;
      transition: all .3s cubic-bezier(.645, .045, .355, 1);
      transform-origin: 100% 50%;
      &:before {
        transform: scale(.6);
        display: inline-block;
        vertical-align: -3px;
      }
      &:hover {
        background-color: #b4bccc;
        color: #fff;
      }
    }
  }
}
</style>
