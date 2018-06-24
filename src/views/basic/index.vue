<template>
  <div class="basic">
    <!--<p>{{msg}}</p>-->
    <div>
      <basicSupplier></basicSupplier>
    </div>
  </div>
</template>

<script>
  import { mapGetters } from 'vuex'
  import basicSupplier from './basicsupplier'
  export default {
    name: 'basic',
    components: { basicSupplier },
    data() {
      return {
        msg: '供应商分类'
      }
    },
    computed: {
      ...mapGetters([
        'roles'
      ])
    }
  }
</script>

<style lang="scss">
  .basic{
    p{
      margin: 25px 0 0 10px;
      font-size: 12px;
    }
  }
</style>
