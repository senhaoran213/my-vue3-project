<template>
  <view class="flash-container">
    <!-- 顶部广告横幅 -->
    <view class="banner">
      <view class="banner-left">
        <view class="banner-title">
          <text class="title-main">主理人脸</text>
          <text class="title-sub">年包已上线</text>
          <view class="banner-eyes">
            <image src="/static/images/venue/eyes.png" mode="widthFix" class="eyes-img"></image>
          </view>
        </view>
        <view class="banner-desc">前50名购买年卡的主理人可获得场馆赠20次</view>
      </view>
      <view class="banner-right">
        <view class="right-item">4款套餐任您挑选</view>
        <view class="right-item">一次购买保障一年</view>
        <view class="right-item">俱乐部专享定制皮肤</view>
        <view class="right-item">更有限定皮肤解锁</view>
      </view>
    </view>

    <!-- 搜索框 -->
    <view class="search-box">
      <view class="search-input">
        <wd-icon name="search" size="4vm" color="#999"></wd-icon>
        <text class="search-placeholder">活动/场馆名称</text>
      </view>
      <view class="search-button">点击下滑购买 >>></view>
      <view class="promote-button">
        <wd-icon name="fire" size="4vm" color="#fff"></wd-icon>
        <text>我要推广</text>
      </view>
    </view>

    <!-- 运动分类 -->
    <scroll-view scroll-x class="category-scroll" :show-scrollbar="false">
      <view class="category-list">
        <view class="category-item active">
          <view class="category-icon">👍</view>
          <text class="category-text">推荐</text>
        </view>
        <view class="category-item">
          <view class="category-icon">🏸</view>
          <text class="category-text">羽毛球</text>
        </view>
        <view class="category-item">
          <view class="category-icon">🏆</view>
          <text class="category-text">生活</text>
        </view>
        <view class="category-item">
          <view class="category-icon">⚽</view>
          <text class="category-text">足球</text>
        </view>
        <view class="category-item">
          <view class="category-icon">🏊</view>
          <text class="category-text">飞镖</text>
        </view>
      </view>
    </scroll-view>

    <!-- 日期选择 -->
    <scroll-view scroll-x class="date-scroll" :show-scrollbar="false">
      <view class="date-list">
        <view class="date-header">
          <text class="date-day">今日</text>
          <text class="date-day">周日</text>
          <text class="date-day">周一</text>
          <text class="date-day">周二</text>
          <text class="date-day">周三</text>
          <text class="date-day">周四</text>
          <text class="date-day">周五</text>
        </view>
        <view class="date-numbers">
          <view class="date-item active">
            <text>19</text>
          </view>
          <view class="date-item">
            <text>20</text>
          </view>
          <view class="date-item">
            <text>21</text>
          </view>
          <view class="date-item">
            <text>22</text>
          </view>
          <view class="date-item">
            <text>23</text>
          </view>
          <view class="date-item">
            <text>24</text>
          </view>
          <view class="date-item">
            <text>25</text>
          </view>
        </view>
      </view>
    </scroll-view>

    <!-- 筛选条件 -->
    <view class="filter-bar">
      <view class="filter-item">
        <text>智能排序</text>
        <wd-icon name="arrow-down" size="3vm" color="#666"></wd-icon>
      </view>
      <view class="filter-item">
        <text>全城</text>
        <wd-icon name="arrow-down" size="3vm" color="#666"></wd-icon>
      </view>
    </view>

    <!-- 活动列表 -->
    <view class="activity-list">
      <!-- 活动项目1 -->
      <wd-card custom-class="activity-card">
        <view class="activity-item">
          <view class="activity-title">豪城4月19日晚上畅打</view>
          <view class="activity-info">
            <view class="activity-location">
              <wd-icon name="location" size="3.5vm" color="#999"></wd-icon>
              <text>豪城羽毛球交流中心</text>
              <text class="activity-distance">| 3.7km</text>
            </view>
            <view class="activity-time">
              <wd-icon name="clock" size="3.5vm" color="#999"></wd-icon>
              <text>04月19日 周六 19:00-22:00</text>
            </view>
          </view>
          <view class="activity-footer">
            <view class="avatar-list">
              <view class="avatar-item" v-for="n in 5" :key="n">
                <wd-img width="6.5vm" height="6.5vm" round :src="`/static/images/avatar${n}.png`"></wd-img>
              </view>
              <view class="avatar-more">...</view>
            </view>
            <view class="activity-status">
              <view class="status-text">报名中 14/18</view>
              <view class="level-text">L1-L8</view>
            </view>
            <view class="activity-venue">
              <wd-img width="8vm" height="8vm" src="/static/images/venue/venue1.png"></wd-img>
              <text>豪城运动羽毛球交流中心</text>
            </view>
            <view class="signup-button">
              去报名
            </view>
          </view>
        </view>
      </wd-card>

      <!-- 活动项目2 -->
      <wd-card custom-class="activity-card">
        <view class="activity-item">
          <view class="activity-title">羽嗨俱乐部-宝龙极致馆</view>
          <view class="activity-info">
            <view class="activity-location">
              <wd-icon name="location" size="3.5vm" color="#999"></wd-icon>
              <text>威克多·极致羽毛球馆(宁化地铁店)</text>
              <text class="activity-distance">| 3.4km</text>
            </view>
            <view class="activity-time">
              <wd-icon name="clock" size="3.5vm" color="#999"></wd-icon>
              <text>04月20日 周日 07:00-10:00</text>
            </view>
          </view>
          <view class="activity-footer">
            <view class="avatar-list">
              <view class="avatar-item" v-for="n in 5" :key="n">
                <wd-img width="6.5vm" height="6.5vm" round :src="`/static/images/avatar${n}.png`"></wd-img>
              </view>
              <view class="avatar-more">...</view>
            </view>
            <view class="activity-status">
              <view class="status-text">报名中 11/42</view>
              <view class="level-text">L1-L8</view>
            </view>
            <view class="activity-venue">
              <wd-img width="8vm" height="8vm" src="/static/images/venue/venue2.png"></wd-img>
              <view class="price-tag">
                <text>¥</text>
                <view class="price-icon">
                  <wd-icon name="cart" size="3.5vm" color="#fff"></wd-icon>
                </view>
                <text>闪购特惠</text>
              </view>
            </view>
            <view class="signup-button">
              去报名
            </view>
          </view>
        </view>
      </wd-card>
    </view>

    <!-- 底部占位 -->
    <view class="tabbar-placeholder"></view>
  </view>
</template>

<script setup lang="ts">
import { ref, reactive } from 'vue';

// 页面逻辑可以根据需要添加
</script>

<style lang="scss" scoped>
/* 所有尺寸都使用vm单位 */
.flash-container {
  padding: 0 3vm;
  background-color: #f5f5f5;
  min-height: 100vh;
}

/* 顶部广告横幅 */
.banner {
  margin-top: 3vm;
  display: flex;
  background: linear-gradient(135deg, #ffd500, #75f7ff);
  border-radius: 3vm;
  padding: 3vm;
  margin-bottom: 3vm;
  position: relative;
  overflow: hidden;

  .banner-left {
    flex: 3;
    
    .banner-title {
      position: relative;
      margin-bottom: 2vm;
      
      .title-main {
        font-size: 5.5vm;
        font-weight: bold;
        color: #000;
        line-height: 1.2;
        display: block;
      }
      
      .title-sub {
        font-size: 5.5vm;
        font-weight: bold;
        color: #28ce26;
        line-height: 1.2;
        display: block;
      }

      .banner-eyes {
        position: absolute;
        top: 1vm;
        right: 20%;
        
        .eyes-img {
          width: 6vm;
        }
      }
    }
    
    .banner-desc {
      font-size: 3vm;
      color: #333;
      margin-bottom: 2vm;
    }
  }
  
  .banner-right {
    flex: 2;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    
    .right-item {
      background-color: rgba(255, 255, 255, 0.7);
      padding: 1vm 2vm;
      border-radius: 1vm;
      font-size: 2.6vm;
      margin-bottom: 1vm;
      color: #333;
    }
  }
}

/* 搜索框 */
.search-box {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 3vm;
  
  .search-input {
    display: flex;
    align-items: center;
    background-color: #f0f0f0;
    padding: 2vm 3vm;
    border-radius: 6vm;
    flex: 1;
    
    .search-placeholder {
      color: #999;
      margin-left: 1vm;
      font-size: 3.2vm;
    }
  }
  
  .search-button {
    background-color: #333;
    color: #fff;
    font-size: 2.8vm;
    padding: 1.5vm 2.5vm;
    border-radius: 6vm;
    margin: 0 2vm;
  }
  
  .promote-button {
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: #f24949;
    padding: 1.5vm 2.5vm;
    border-radius: 6vm;
    
    text {
      color: #fff;
      margin-left: 1vm;
      font-size: 2.8vm;
    }
  }
}

/* 运动分类 */
.category-scroll {
  white-space: nowrap;
  margin-bottom: 3vm;
  
  .category-list {
    display: flex;
    padding: 1vm 0;
    
    .category-item {
      display: inline-flex;
      flex-direction: column;
      align-items: center;
      margin-right: 6vm;
      
      &.active {
        .category-text {
          color: #00cdff;
          font-weight: bold;
        }
        
        .category-icon {
          position: relative;
          
          &::after {
            content: '';
            position: absolute;
            bottom: -1vm;
            left: 50%;
            transform: translateX(-50%);
            width: 5vm;
            height: 0.5vm;
            background-color: #00cdff;
            border-radius: 0.5vm;
          }
        }
      }
      
      .category-icon {
        font-size: 5vm;
        margin-bottom: 1vm;
      }
      
      .category-text {
        font-size: 3vm;
        color: #666;
      }
    }
  }
}

/* 日期选择 */
.date-scroll {
  margin-bottom: 2vm;
  background-color: #fff;
  padding: 2vm 0;
  border-radius: 2vm;
  
  .date-list {
    .date-header {
      display: flex;
      justify-content: space-around;
      margin-bottom: 1vm;
      
      .date-day {
        font-size: 2.8vm;
        color: #666;
        width: 12vm;
        text-align: center;
      }
    }
    
    .date-numbers {
      display: flex;
      justify-content: space-around;
      
      .date-item {
        width: 8vm;
        height: 8vm;
        display: flex;
        align-items: center;
        justify-content: center;
        border-radius: 50%;
        font-size: 3.2vm;
        color: #333;
        
        &.active {
          background-color: #00cdff;
          color: #fff;
        }
      }
    }
  }
}

/* 筛选条件 */
.filter-bar {
  display: flex;
  align-items: center;
  padding: 2vm 0;
  margin-bottom: 2vm;
  
  .filter-item {
    display: flex;
    align-items: center;
    margin-right: 4vm;
    font-size: 3vm;
    color: #666;
    
    text {
      margin-right: 1vm;
    }
  }
}

/* 活动列表 */
.activity-list {
  margin-bottom: 20vm;
  
  :deep(.activity-card) {
    margin-bottom: 3vm;
    border-radius: 3vm !important;
    overflow: hidden;
  }
  
  .activity-item {
    .activity-title {
      font-size: 4vm;
      font-weight: 600;
      color: #333;
      margin-bottom: 2vm;
    }
    
    .activity-info {
      margin-bottom: 2vm;
      
      .activity-location, .activity-time {
        display: flex;
        align-items: center;
        margin-bottom: 1vm;
        font-size: 3vm;
        color: #666;
        
        text {
          margin-left: 1vm;
        }
        
        .activity-distance {
          color: #999;
          margin-left: 1vm;
        }
      }
    }
    
    .activity-footer {
      display: flex;
      flex-direction: column;
      
      .avatar-list {
        display: flex;
        align-items: center;
        margin-bottom: 2vm;
        
        .avatar-item {
          margin-right: -1.5vm;
          border: 0.2vm solid #fff;
          border-radius: 50%;
        }
        
        .avatar-more {
          width: 6.5vm;
          height: 6.5vm;
          background-color: #f0f0f0;
          color: #999;
          display: flex;
          align-items: center;
          justify-content: center;
          border-radius: 50%;
          margin-left: 2vm;
          font-size: 3vm;
        }
      }
      
      .activity-status {
        display: flex;
        justify-content: space-between;
        margin-bottom: 2vm;
        
        .status-text {
          color: #00cdff;
          font-size: 3vm;
        }
        
        .level-text {
          color: #00cdff;
          font-size: 3vm;
        }
      }
      
      .activity-venue {
        display: flex;
        align-items: center;
        margin-bottom: 2vm;
        
        text {
          margin-left: 2vm;
          font-size: 3vm;
          color: #666;
        }
        
        .price-tag {
          margin-left: 2vm;
          display: flex;
          align-items: center;
          color: #ff5722;
          font-size: 3vm;
          
          .price-icon {
            background-color: #ff5722;
            border-radius: 1vm;
            margin: 0 0.5vm;
          }
        }
      }
      
      .signup-button {
        align-self: flex-end;
        background-color: #00cdff;
        color: #fff;
        font-size: 3.2vm;
        padding: 1.5vm 5vm;
        border-radius: 6vm;
      }
    }
  }
}

/* 底部占位 */
.tabbar-placeholder {
  height: 13vm;
}
</style>
