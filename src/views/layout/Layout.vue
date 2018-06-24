<template>
	<div class="app-wrapper">
		<!-- <sidebar class="sidebar-container"></sidebar> -->
		<div class="main-container">
			<navbar></navbar>
			<tags-view></tags-view>
			<keep-alive>
				<app-main></app-main>
			</keep-alive>
		</div>
	</div>
</template>

<script>
import { Navbar, AppMain, TagsView } from 'views/layout/components'

export default {
  name: 'layout',
  components: {
    Navbar,
    // Sidebar,
    AppMain,
    TagsView
  },
  computed: {
    // sidebar() {
    //   return this.$store.state.app.sidebar
    // }
  }
}
</script>

<style rel="stylesheet/scss" lang="scss" scoped>
	@import "src/styles/mixin.scss";
	.app-wrapper {
	  @include clearfix;
	  position: relative;
	  height: 100%;
	  width: 100%;
	}
</style>
