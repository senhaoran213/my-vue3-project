<template>
  <view class="flash-container">
    <!-- 顶部导航栏 -->
    <wd-navbar title="闪动">
      <template #right>
        <view class="navbar-right">
          <wd-icon name="search" size="20px" color="#333"></wd-icon>
          <wd-icon name="add" size="20px" color="#333" class="add-icon"></wd-icon>
        </view>
      </template>
    </wd-navbar>

    <!-- 搜索栏 -->
    <view class="search-box">
      <wd-search v-model="searchValue" placeholder="搜索活动" cancel-txt=" "></wd-search>
    </view>

    <!-- 活动类型标签页 -->
    <wd-tabs v-model="activeTab" class="type-tabs">
      <wd-tab title="推荐"></wd-tab>
      <wd-tab title="羽毛球"></wd-tab>
      <wd-tab title="篮球"></wd-tab>
      <wd-tab title="足球"></wd-tab>
      <wd-tab title="网球"></wd-tab>
      <wd-tab title="飞盘"></wd-tab>
    </wd-tabs>

    <!-- 活动列表 -->
    <view class="activity-list">
      <wd-card v-for="(activity, index) in activities" :key="index" custom-class="activity-card">
        <view class="activity-item">
          <!-- 活动图片 -->
          <view class="activity-image">
            <wd-img :src="activity.image" width="100%" height="180px" mode="aspectFill"></wd-img>
            <view class="activity-tag" :class="activity.tagClass">{{ activity.tag }}</view>
          </view>
          
          <!-- 活动信息 -->
          <view class="activity-info">
            <view class="activity-title">{{ activity.title }}</view>
            <view class="activity-desc">{{ activity.description }}</view>
            
            <!-- 活动详情 -->
            <view class="activity-details">
              <view class="detail-item">
                <wd-icon name="location" size="16px" color="#999"></wd-icon>
                <text>{{ activity.location }}</text>
              </view>
              <view class="detail-item">
                <wd-icon name="time" size="16px" color="#999"></wd-icon>
                <text>{{ activity.time }}</text>
              </view>
            </view>
            
            <!-- 活动状态 -->
            <view class="activity-status">
              <view class="status-tag" :class="activity.statusClass">
                {{ activity.status }}
              </view>
              <view class="price">¥{{ activity.price }}</view>
            </view>
          </view>
          
          <!-- 活动底部 -->
          <view class="activity-footer">
            <view class="participants">
              <view class="avatar-group">
                <wd-img 
                  v-for="(avatar, idx) in activity.avatars" 
                  :key="idx"
                  :src="avatar"
                  width="24"
                  height="24"
                  round
                  :style="{ marginLeft: idx > 0 ? '-8px' : '0' }"
                ></wd-img>
              </view>
              <text class="participant-count">{{ activity.participantCount }}人已报名</text>
            </view>
            <wd-button 
              size="small" 
              :type="activity.status === '报名中' ? 'primary' : 'info'"
              :disabled="activity.status !== '报名中'"
            >
              {{ activity.status === '报名中' ? '立即报名' : '已结束' }}
            </wd-button>
          </view>
        </view>
      </wd-card>
    </view>

    <!-- 底部悬浮按钮 -->
    <view class="float-btn">
      <wd-button circle type="primary">
        <wd-icon name="add" size="24px" color="#fff"></wd-icon>
      </wd-button>
    </view>
  </view>
</template>

<script setup lang="ts">
import { ref, reactive } from 'vue';

// 搜索值
const searchValue = ref('');

// 标签页激活索引
const activeTab = ref(0);

// 活动数据
const activities = reactive([
  {
    id: 1,
    title: '周末羽毛球活动',
    description: '专业教练指导，适合各水平球友',
    image: '/static/images/activity/activity1.png',
    location: '北京朝阳体育馆',
    time: '2024-04-27 14:00',
    price: 88,
    tag: '热门',
    tagClass: 'hot',
    status: '报名中',
    statusClass: 'active',
    participantCount: 12,
    avatars: [
      '/static/images/avatar/avatar1.png',
      '/static/images/avatar/avatar2.png',
      '/static/images/avatar/avatar3.png'
    ]
  },
  {
    id: 2,
    title: '篮球友谊赛',
    description: '5v5全场，欢迎篮球爱好者',
    image: '/static/images/activity/activity2.png',
    location: '上海浦东体育馆',
    time: '2024-04-28 19:00',
    price: 68,
    tag: '新活动',
    tagClass: 'new',
    status: '报名中',
    statusClass: 'active',
    participantCount: 8,
    avatars: [
      '/static/images/avatar/avatar4.png',
      '/static/images/avatar/avatar5.png'
    ]
  },
  {
    id: 3,
    title: '网球训练营',
    description: '专业教练一对一指导',
    image: '/static/images/activity/activity3.png',
    location: '广州天河体育中心',
    time: '2024-04-29 15:00',
    price: 128,
    tag: '精品',
    tagClass: 'premium',
    status: '已结束',
    statusClass: 'ended',
    participantCount: 15,
    avatars: [
      '/static/images/avatar/avatar1.png',
      '/static/images/avatar/avatar2.png',
      '/static/images/avatar/avatar3.png',
      '/static/images/avatar/avatar4.png'
    ]
  }
]);
</script>

<style lang="scss" scoped>
.flash-container {
  min-height: 100vh;
  background: linear-gradient(135deg, #f7f4ff 0%, #e9e6ff 100%);
  padding-bottom: 80px;
}

.navbar-right {
  display: flex;
  align-items: center;
  
  .add-icon {
    margin-left: 15px;
  }
}

.search-box {
  padding: 10px 15px;
  background-color: #fff;
}

.type-tabs {
  background-color: #fff;
  margin-bottom: 10px;
}

.activity-list {
  padding: 0 15px;
}

.activity-card {
  margin-bottom: 15px;
  border-radius: 12px !important;
  overflow: hidden;
  
  .activity-item {
    .activity-image {
      position: relative;
      
      .activity-tag {
        position: absolute;
        top: 10px;
        right: 10px;
        padding: 4px 8px;
        border-radius: 4px;
        font-size: 12px;
        color: #fff;
        
        &.hot {
          background-color: #ff4d4f;
        }
        
        &.new {
          background-color: #52c41a;
        }
        
        &.premium {
          background-color: #faad14;
        }
      }
    }
    
    .activity-info {
      padding: 15px;
      
      .activity-title {
        font-size: 16px;
        font-weight: 500;
        color: #333;
        margin-bottom: 8px;
      }
      
      .activity-desc {
        font-size: 14px;
        color: #666;
        margin-bottom: 12px;
      }
      
      .activity-details {
        display: flex;
        flex-direction: column;
        gap: 8px;
        margin-bottom: 12px;
        
        .detail-item {
          display: flex;
          align-items: center;
          font-size: 12px;
          color: #999;
          
          text {
            margin-left: 4px;
          }
        }
      }
      
      .activity-status {
        display: flex;
        justify-content: space-between;
        align-items: center;
        
        .status-tag {
          padding: 2px 8px;
          border-radius: 4px;
          font-size: 12px;
          
          &.active {
            background-color: #e6f7ff;
            color: #1890ff;
          }
          
          &.ended {
            background-color: #f5f5f5;
            color: #999;
          }
        }
        
        .price {
          font-size: 16px;
          font-weight: 500;
          color: #ff4d4f;
        }
      }
    }
    
    .activity-footer {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 12px 15px;
      border-top: 1px solid #f5f5f5;
      
      .participants {
        display: flex;
        align-items: center;
        
        .avatar-group {
          display: flex;
          margin-right: 8px;
        }
        
        .participant-count {
          font-size: 12px;
          color: #999;
        }
      }
    }
  }
}

.float-btn {
  position: fixed;
  right: 20px;
  bottom: 80px;
  z-index: 999;
}
</style>
