<template>
    <div class="style-page">
        <AppBar title="BallPulse"/>
        <div class="style-page-list">
            <EasyRefresh
                    :userSelect="false"
                    :onRefresh="onRefresh"
                    :loadMore="loadMore">
                <template v-slot:header>
                    <BallPulseHeader/>
                </template>
                <StripeList :count="itemCount"/>
                <template v-slot:footer>
                    <BallPulseFooter/>
                </template>
            </EasyRefresh>
        </div>
    </div>
</template>

<script lang="ts">
    import {Component, Vue} from 'vue-property-decorator'
    import AppBar from '../../components/AppBar.vue'
    import StripeList from '../../components/StripeList.vue'

    /**
     * BallPulse样式
     */
    @Component({
        components: {
            AppBar,
            StripeList,
        },
    })
    export default class BallPulsePage extends Vue {
        // 条目数量
        private itemCount: number = 20
        // 刷新
        private onRefresh(done: () => void) {
            setTimeout(() => {
                this.itemCount = 20
                done()
            }, 1000)
        }
        // 加载更多
        private loadMore(done: (noMore: boolean) => void) {
            setTimeout(() => {
                if (this.itemCount >= 40) {
                    done(true)
                } else {
                    this.itemCount += 10
                    done(false)
                }
            }, 1000)
        }
    }
</script>

<style lang="scss">
    .style-page {
        width: 100%;
        height: 100%;
        .style-page-list {
            width: 100%;
            height: calc(100% - 60px);
        }
    }
</style>
