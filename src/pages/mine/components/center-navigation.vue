<template>
    <view class="contain">
        <wd-card>
            <template #default>
                    <view class="navi-items" v-for="(item,index) in naviLists" :key="index">
                        <image class="items-img" :src="item.navSrc" mode="scaleFit" />
                        <view class="item-name">{{ item.naviName }}</view>
                    </view>

            </template>
        </wd-card>
    </view>
</template>
<script setup lang="ts">
import { ref } from 'vue';
import { type NaviModeDto } from '../interface';
const naviLists = ref < NaviModeDto[] > ([{
    naviName: '我的订单',
    navSrc: '/static/images/mine/navi-1.png'
}, {
    naviName: '我的钱包',
    navSrc: '/static/images/mine/navi-2.png'
}, {
    naviName: '我的卡券',
    navSrc: '/static/images/mine/navi-3.png'
}, {
    naviName: '工具箱',
    navSrc: '/static/images/mine/navi-4.png'
}, {
    naviName: '活动数据',
    navSrc: '/static/images/mine/navi-5.png'
}])
</script>
<style scoped lang='scss'>
.contain {
    .wd-card {
        padding: 15px 10px;
        box-sizing: border-box;
        overflow-x: scroll;
        display: flex;
            :deep(.wd-card__content){
                display: flex;
                .navi-items {
                display: flex;
                flex-direction: column;
                align-items: center;
                width: 100px;
                .items-img {
                    width: 35px;
                    height: 35px;
                    margin-bottom: 8px;
                }

        }

            }
        
    }
}
</style>
