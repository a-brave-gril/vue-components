<template>
  <layout>
    <x-nav slot="header">
      <div slot="title">Search</div>
    </x-nav>
    <x-body slot="body"  class="demos img-demos">
      <search :value="value" placeholder="搜索商品/商店/用户"
        @on-submit="submitHandler"
        @input="inputHandler"
        @on-change="inputHandler">
        <div slot="keywords">
          <span class="keyword">
            上海
          </span>
          <span class="keyword">
            武汉
          </span>
          <span class="keyword">
            深圳
          </span>
          <span class="keyword">
            南京
          </span>
          <span class="keyword">
            北京
          </span>
        </div>
        <div slot="result" style="text-align:center;padding:15px">
          搜索结果显示
        </div>
      </search>
    </x-body>
  </layout>
</template>

<script>
export default {
  methods: {
    inputHandler (value) {
      this.value = value
    },
    submitHandler (value) {
      console.log('submitHandler')
    }
  },
  data () {
    return {
      value: ''
    }
  }
}
</script>

<style lang="scss">
  
</style>
