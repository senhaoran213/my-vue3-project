<template>
  <view class="club-container">
    <!-- 顶部导航栏 -->
    <wd-navbar title="我的俱乐部">
      <template #right>
        <view class="navbar-right">
          <wd-icon name="more" size="20px" color="#333"></wd-icon>
          <wd-icon name="add" size="20px" color="#333" class="add-icon"></wd-icon>
        </view>
      </template>
    </wd-navbar>

    <!-- 搜索栏 -->
    <view class="search-box">
      <wd-search v-model="searchValue" placeholder="搜索俱乐部" cancel-txt=" "></wd-search>
    </view>

    <!-- 标签页 -->
    <wd-tabs v-model="activeTab" style="margin-bottom: 10px;">
      <wd-tab title="我的俱乐部"></wd-tab>
      <wd-tab title="全部俱乐部"></wd-tab>
    </wd-tabs>

    <!-- 空状态 -->
    <view v-if="activeTab === 0 && !hasClubs" class="empty-state">
      <image src="/static/images/club/empty.png" mode="aspectFit" class="empty-image"></image>
      <view class="empty-text">暂未加入俱乐部</view>
      <view class="empty-desc">为您推荐以下俱乐部，或者创建一个俱乐部</view>
      <wd-button type="primary" class="create-btn" @click="handleCreateClub">
        <wd-icon name="add" size="16px" color="#fff"></wd-icon>
        创建俱乐部
      </wd-button>
    </view>

    <!-- 热门俱乐部 -->
    <view class="hot-clubs-section">
      <view class="section-title">热门俱乐部</view>
      <view class="club-list">
        <wd-card v-for="(club, index) in hotClubs" :key="index" custom-class="club-card">
          <view class="club-item">
            <view class="club-header">
              <wd-img :src="club.image" width="80" height="80" round></wd-img>
              <view class="club-info">
                <view class="club-name">{{ club.name }}</view>
                <view class="club-tags">
                  <view v-for="(tag, tagIndex) in club.tags" :key="tagIndex" class="club-tag">
                    {{ tag }}
                  </view>
                </view>
              </view>
              <view class="club-stats">
                <wd-badge :value="club.members" type="primary"></wd-badge>
              </view>
            </view>
            <view class="club-desc">
              <view class="club-location">
                <wd-icon name="location" size="16px" color="#999"></wd-icon>
                <text>{{ club.location }}</text>
              </view>
            </view>
            <view class="club-footer">
              <view class="club-id">
                <text>合作｜团建: {{ club.id }}</text>
              </view>
              <wd-button size="small" custom-class="join-btn" @click="handleJoinClub(club)">+ 加入</wd-button>
            </view>
          </view>
        </wd-card>
      </view>
    </view>

    <!-- 右下角悬浮按钮 -->
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

// 是否有加入的俱乐部
const hasClubs = ref(false);

// 热门俱乐部数据
const hotClubs = reactive([
  {
    id: '150108185',
    name: 'AI飞盘',
    image: '/static/images/club/club1.png',
    tags: ['飞盘', '网球'],
    members: 56364,
    location: '北京AI 俱乐部',
    description: '86 AI飞盘，是一个很好的俱乐部，欢迎加入！'
  },
  {
    id: '20121101',
    name: '乐天派',
    image: '/static/images/club/club2.png',
    tags: ['羽毛球', '生活'],
    members: 58248,
    location: '北京朝阳区',
    description: '乐天派，2012年11月创办，创始人：赖姐，欢迎各位朋友加入！'
  },
  {
    id: '20150506',
    name: '飞跃俱乐部',
    image: '/static/images/club/club3.png',
    tags: ['篮球', '足球'],
    members: 38232,
    location: '上海市浦东新区',
    description: '专业体育爱好者聚集地，定期组织比赛和活动'
  }
]);

// 处理创建俱乐部
const handleCreateClub = () => {
  uni.showToast({
    title: '创建俱乐部功能开发中',
    icon: 'none'
  });
};

// 处理加入俱乐部
const handleJoinClub = (club: any) => {
  uni.showToast({
    title: `已申请加入${club.name}`,
    icon: 'none'
  });
};
</script>

<style lang="scss" scoped>
.club-container {
  min-height: 100vh;
  background-color: #f5f5f5;
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

.empty-state {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 40px 0;
  background-color: #fff;
  margin-bottom: 15px;
  
  .empty-image {
    width: 120px;
    height: 120px;
    margin-bottom: 15px;
  }
  
  .empty-text {
    font-size: 16px;
    font-weight: 500;
    color: #333;
    margin-bottom: 8px;
  }
  
  .empty-desc {
    font-size: 14px;
    color: #999;
    margin-bottom: 20px;
    text-align: center;
    padding: 0 30px;
  }
  
  .create-btn {
    width: 160px;
    border-radius: 20px;
  }
}

.hot-clubs-section {
  padding: 0 15px;
  
  .section-title {
    font-size: 16px;
    font-weight: 500;
    color: #333;
    margin-bottom: 10px;
  }
  
  .club-list {
    display: flex;
    flex-direction: column;
  }
  
  :deep(.club-card) {
    margin-bottom: 15px;
    border-radius: 8px !important;
    overflow: hidden;
  }
  
  .club-item {
    .club-header {
      display: flex;
      margin-bottom: 10px;
      
      .club-info {
        flex: 1;
        margin-left: 10px;
        
        .club-name {
          font-size: 16px;
          font-weight: 500;
          color: #333;
          margin-bottom: 5px;
        }
        
        .club-tags {
          display: flex;
          flex-wrap: wrap;
          
          .club-tag {
            background-color: #f5f5f5;
            color: #666;
            font-size: 12px;
            padding: 2px 6px;
            border-radius: 4px;
            margin-right: 5px;
          }
        }
      }
    }
    
    .club-desc {
      margin-bottom: 10px;
      
      .club-location {
        display: flex;
        align-items: center;
        font-size: 12px;
        color: #999;
        
        text {
          margin-left: 5px;
        }
      }
    }
    
    .club-footer {
      display: flex;
      justify-content: space-between;
      align-items: center;
      
      .club-id {
        font-size: 12px;
        color: #999;
      }
      
      .join-btn {
        background-color: #f2f2f2;
        color: #666;
        border: none;
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