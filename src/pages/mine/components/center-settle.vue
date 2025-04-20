<template>
    <view class="contain">
        <wd-card v-for="(item,index) in settleModeLists" :key="index">
            <template #default>
                <view class="mode">
                    <view class="mode-left">
                        <image
                            class="items-img"
                            :src="item.navSrc"
                            mode="scaleToFill"
                        />
                    </view>
                    <view class="mode-right">
                        <view style="font-size:3vw;">我要推广</view>
                        <view style="font-size: 2.5vw;">提高曝光</view>
                    </view>
                </view>
            </template>
        </wd-card>
    </view>
</template>
<script setup lang="ts">
import { type SettleModeDto } from '../interface';
import { ref } from 'vue';
const settleModeLists = ref<SettleModeDto[]>([{
    title:'我要推广',
    smallTitle:'提高曝光',
    navSrc:'/static/images/mine/settle-1.png'
},{
    title:'邀请入驻',
    smallTitle:'一起动起来',
    navSrc:'/static/images/mine/settle-2.png'
},{
    title:'场馆入驻',
    smallTitle:'申请入驻平台',
    navSrc:'/static/images/mine/settle-3.png'
}])
</script>
<style scoped lang='scss'>
.contain {
    overflow: hidden;
    display: flex;
    overflow: auto;
    box-sizing: border-box;
    justify-content: space-between;

    :deep(.wd-card) {
        padding: 5px;
        width: 50vw !important;
        .wd-card__content {
            padding: 5px;
            box-sizing: border-box;
            .mode{
                display: flex;
                align-items: center;
                .mode-left{
                    .items-img{
                        width: 8.5vw;
                        height: 8.5vw;
                    }
                }
            }
        }

    }


}
</style>
