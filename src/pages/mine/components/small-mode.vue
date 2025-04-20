<template>
    <view class="mode">
        <view class="mode-top">
            <view class="small-icon">
                <wd-img :width="20" :height="20" :src="props.smallModeList.imgUrl" />
            </view>
            <view class="name">{{ props.smallModeList.name }}</view>
            <view class="right-arrow">></view>
        </view>
        <view class="mode-bottom">{{ props.smallModeList.count }}
            <text>{{ props.smallModeList.unit }}</text>
        </view>
    </view>
</template>
<script setup lang="ts">
import { type SmallModeDto } from '../interface';
import { withDefaults } from 'vue';
const props = withDefaults(defineProps<{
    smallModeList: SmallModeDto
}>(), {
    smallModeList: () => ({
        unit: '次',
        count: 0,
        imgUrl: '/static/images/small-images/prize.png',
        name: '活动'
    })
})
</script>
<style scoped lang='scss'>
.mode {
    .mode-top {
        display: flex;
        align-items: center;

        .name {
            margin-left: 1vw;
        }

        .right-arrow {
            margin-left: 1vw;
        }
    }

    .mode-bottom {
        font-size: 4vw;

        text {
            font-size: 3vw;
        }
    }
}
</style>
