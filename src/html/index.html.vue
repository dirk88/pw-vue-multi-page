<template>
  <div id="app">
    <mu-paper :zDepth="5" style="position:fixed;bottom:0;left:0;width:100%">
      <mu-bottom-nav :value="bottomNav" @change="handleChange">
        <mu-bottom-nav-item href="m/index.html" value="recents" title="首页" icon="restore"/>
        <mu-bottom-nav-item href="pc/order.html" value="favorites" title="pc页面" icon="favorite"/>
        <mu-bottom-nav-item value="nearby" title="Nearby" icon="location_on"/>
      </mu-bottom-nav>
    </mu-paper>
  </div>
</template>

<script>
    import lib from '@/assets/js/lib.js'

    export default {
        data () {
            const list = []
            for (let i = 0; i < 10; i++) {
                list.push('item' + (i + 1))
            }
            return {
                bottomNav: 'recents',
                list,
                num: 10,
                refreshing: false,
                trigger: null,
                loading: false,
                scroller: null,
            }
        },

        mounted () {
            this.trigger = this.$el
            this.$el.style.height=window.screen.height+'px'
            this.scroller = this.$el
        },
        methods:{
            handleChange (val) {
                this.bottomNav = val
            },
            refresh () {
                this.refreshing = true
                setTimeout(() => {
                    const list = []
                    for (let i = this.num; i < this.num + 10; i++) {
                        list.push('item' + (i + 1))
                    }
                    this.list = list
                    this.num += 10
                    this.refreshing = false
                }, 2000)
            },
            loadMore () {
                this.loading = true
                setTimeout(() => {
                    for (let i = this.num; i < this.num + 10; i++) {
                        this.list.push('item' + (i + 1))
                    }
                    this.num += 10
                    this.loading = false
                }, 2000)
            }
        },
        components: {

        }
    }
</script>

<style lang="stylus">
  #app
    position:relative;
    height:100%;
    width:100%;
    overflow: auto;
    -webkit-overflow-scrolling: touch;
  .icon
    vertical-align:middle;
  .mu-card-actions
    text-align:right;
  .mu-infinite-scroll
    padding-top:8px;
    padding-bottom:0!important;

</style>

