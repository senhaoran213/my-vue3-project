<template>
    <view class="contain">
        <view class="contain-in">
            <view class="text">
                <text class="bigTitle">2025招行北分员工</text>
                <text class="smallTitle">体育锻炼项目</text>
            </view>
            <view class="use-btn">
                <text>立即使用</text>
            </view>
        </view>
    </view>
</template>
<script setup lang="ts">

</script>
<style scoped lang='scss'>
.contain {
    padding: 15px 10px;
    box-sizing: border-box;

    .contain-in {
        background-color: #ff5f4e;
        height: 70px;
        border-radius: 30px;
        display: flex;
        justify-content: space-around;
        align-items: center;

        .text {
            display: flex;
            flex-direction: column;
            align-items: center;

            .bigTitle {
                font-size: 2.5vw;
            }

            .smallTitle {
                font-size: 4vw;
            }
        }

        .use-btn {
            display: flex;
            align-items: center;
            justify-content: center;
            background-color: yellow;
            color: #ff5f4e;
            font-weight: 900;
            height: 8vw;
            width: 20vw;
            border-radius: 20px;
        }
    }


}
</style>
