<template>
    <view class="contain">
        <wd-card>
            <template #title>
                <view class="title">
                    <view class="title_price">价格：XXX</view>
                </view>
            </template>
        </wd-card>
    </view>
</template>
<script setup lang="ts">

</script>
<style scoped lang='scss'>
:deep(.wd-card) {
    padding: 0px !important;

    .wd-card__title-content {
        padding: 0px;

        .title {
            height: 130px;
            width: 100%;
            background-color: rgba(255,0,0,.5);
            position: relative;
            .title_price{
                width: 30%;
                height: 30%;
                background-color: #fff;
                display: flex;
                align-items: center;
                justify-content: center;
                position: absolute;
                left: 0;
                bottom: 0;
            }

        }
    }

}
</style>
