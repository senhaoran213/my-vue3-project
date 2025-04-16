<template>
  <view class="container">
    <wd-navbar>
      <template #left>
        <view class="left-icon">
          <view class="head-icon">
            <uni-icons color="#fff" type="headphones" size="30"></uni-icons>
            <uni-icons color="#fff" type="notification" size="30"></uni-icons>
          </view>
        </view>
      </template>
      <template #right>
        <view class="right-icon">
          <view>
            <uni-icons color="#fff" type="more-filled" size="30"></uni-icons>
          </view>
          <view>
            <wd-icon color="#fff" name="decrease" size="30px"></wd-icon>
          </view>
          <view>
            <uni-icons color="#fff" type="circle-filled" size="30"></uni-icons>
          </view>
        </view>
      </template>
    </wd-navbar>
    <wd-card>
      <template #title>
        <view class="title-top">
          <view class="top-avatar">
            <wd-img :width="80" :height="80" round />
            <view class="top-name">
              <view class="username">
                <text>amli</text>
              </view>
              <view class="be-praised">
                获赞<text>0</text>
              </view>
            </view>
          </view>
          <wd-button plain size="small">编辑资料</wd-button>
        </view>
      </template>
      <template #default>
        <view class="big">
          <small-mode v-for="(item, index) in dataList " :smallModeList="item" :key="index"></small-mode>
        </view>
      </template>
    </wd-card>
  </view>
</template>
<script setup lang="ts">
import { reactive } from 'vue';
import smallMode from './components/small-mode.vue';
import { type smallModeDto } from './interface';

const dataList = reactive<smallModeDto[]>([
  {
    unit: '次',
    count: 0,
    imgUrl: '/static/images/small-images/prize.png',
    name: '活动'
  },
  {
    unit: '个',
    count: 0,
    imgUrl: '/static/images/small-images/club.png',
    name: '俱乐部'
  },
  {
    unit: 'h',
    count: 0,
    imgUrl: '/static/images/small-images/total-time.png',
    name: '累计时长'
  }
])
</script>
<style scoped lang='scss'>
.container {
  background: url('/static/images/mine/mine-bgc.png') top/100% no-repeat;
  height: 1500px;
  padding: 20px 10px 0 10px;
  box-sizing: border-box;

  :deep(.wd-navbar) {
    background-color: transparent;

    .left-icon {
      .head-icon {
        .uniui-headphones:before {
          background-color: rgba(0, 0, 0, .3);
          border-radius: 50%;
        }

        .uniui-notification:before {
          background-color: rgba(0, 0, 0, .3);
          border-radius: 50%;
          margin-left: 3vw;
        }
      }
    }

    .right-icon {
      padding: 2px;
      display: flex;
      align-items: center;

      .uniui-more-filled:before {
        background-color: rgba(0, 0, 0, .3);
        box-sizing: border-box;
        padding: 4px 6px;
        border-top-left-radius: 50%;
        border-bottom-left-radius: 50%;
        border-right: 1px solid rgba(255, 255, 255, .5);
      }

      .wd-icon-decrease:before {
        background-color: rgba(0, 0, 0, .3);
        box-sizing: border-box;
        padding: 4px 2px;
      }

      .uniui-circle-filled:before {
        background-color: rgba(0, 0, 0, .3);
        padding: 4px 6px;
        border-top-right-radius: 50%;
        border-bottom-right-radius: 50%;
        border-left: 1px solid rgba(255, 255, 255, .5);
      }
    }
  }

  :deep(.wd-navbar.is-border::after) {
    height: 0px !important;
  }

  .wd-card {
    margin-top: 65%;
    height: 200px;

    .title-top {
      display: flex;
      justify-content: space-between;

      .top-avatar {
        display: flex;

        .wd-img {
          background-color: green;
          margin-top: -40px;
        }

        .top-name {
          margin-left: 2vw;

          .username {
            font-size: 4vw;
          }

          .be-praised {
            margin-top: 5px;
            font-size: 3vw;
          }
        }
      }

      :deep(.wd-button.is-plain.is-primary) {
        color: #cbcbcb !important;
      }
    }

    .wd-card__content {
      .big {
        display: flex;
        justify-content: space-between
      }
    }
  }
}
</style>
