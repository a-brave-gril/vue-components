<template>
  <div>
    <layout v-show="$route.path == '/cnode'">
      <x-nav slot="header" :back="false">
        <div slot="title">CNode-专业中文社区</div>
        <tab :active="home.active" @on-change="activeHandler">
          <tab-item>
            全部
          </tab-item>
          <tab-item>
            精华
          </tab-item>
          <tab-item>
            分享
          </tab-item>
          <tab-item>
            问答
          </tab-item>
          <tab-item>
            招聘
          </tab-item>
        </tab>
      </x-nav>
      <x-body slot="body" :scroll="false" style="background:#fff">
        <list-view @on-pullup="pullupHandler" @on-pulldown="pulldownHandler" :loading="loading">
          <topic-item v-for="item in topics" :item="item" :key="item.id" />
        </list-view>
      </x-body>
    </layout>
    <router-view></router-view>
  </div>
</template>

<script>
import { mapState } from 'vuex'

const tabs = ['all', 'good', 'share', 'ask', 'job']

import {
  TopicItem
} from './components/index'

export default {
  components: {
    TopicItem
  },
  computed: {
    ...mapState({
      home: state => state.cnode.home
    }),
    loading () {
      return this.home[tabs[this.home.active]].loading
    },
    topics () {
      return this.home[tabs[this.home.active]].data
    }
  },
  created () {
    let tab = tabs[this.home.active]
    if (this.home[tab].data.length === 0) {
      this.$store.dispatch('cnode/home', {
        page: 1,
        tab: tabs[0]
      })
    }
  },
  methods: {
    activeHandler (active) {
      let tab = tabs[active]
      this.$store.dispatch('cnode/home', {
        page: 1,
        tab: tab,
        active: active,
        change: true
      })
    },
    pullupHandler () {
      let tab = tabs[this.home.active]
      this.$store.dispatch('cnode/home', {
        page: this.home[tab].query.page + 1,
        tab: tab
      })
    },
    pulldownHandler () {
      let tab = tabs[this.home.active]
      this.$store.dispatch('cnode/home', {
        page: 1,
        tab: tab
      })
    }
  },
  data () {
    return {}
  }
}
</script>

<style lang="scss">
  .v-flow,.swiper{
    height:100%;
    width:100%;
    position:absolute!important;
  }
</style>
