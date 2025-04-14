<template>
  <view class="mine-container">
    <!-- 顶部状态栏背景 -->
    <view class="bg-gradient">
      <view class="status-bar">
        <text class="time">{{ currentTime }}</text>
        <view class="status-icons">
          <text class="signal-icon">●●●</text>
          <text class="wifi-icon">☰</text>
          <text class="battery-icon">⬜</text>
        </view>
      </view>
      
      <view class="header-controls">
        <view class="left-controls">
          <view class="icon-btn headphone">
            <text class="iconfont">🎧</text>
          </view>
          <view class="icon-btn notification">
            <text class="iconfont">🔔</text>
          </view>
        </view>
        <view class="right-controls">
          <view class="more-btn">
            <text class="dot">●●●</text>
          </view>
          <view class="circle-btn">
            <text class="iconfont">⊕</text>
          </view>
        </view>
      </view>
      
      <!-- 横幅广告区 -->
      <view class="banner-section">
        <view class="banner-content">
          <view class="banner-title">
            <text class="line1">一起运动</text>
            <text class="flash-x">Flash X</text>
          </view>
          <view class="banner-subtitle">
            <text>就来闪动</text>
          </view>
          <view class="banner-tags">
            <text class="tag flash-tag">Flash X</text>
            <text class="tag come-on-tag">Come On!</text>
          </view>
        </view>
      </view>
    </view>
    
    <!-- 用户信息卡片 -->
    <view class="user-card">
      <view class="user-info">
        <view class="avatar">
          <!-- 使用背景色代替图片 -->
        </view>
        <view class="user-data">
          <view class="username">留给中国队的时间...</view>
          <view class="edit-btn">编辑资料</view>
        </view>
      </view>
      <view class="user-stats">
        <text class="stats-count">获赞 0</text>
      </view>
      
      <!-- 用户活动数据 -->
      <view class="activity-data">
        <view class="data-item">
          <view class="data-icon trophy">🏆</view>
          <text class="data-label">活动</text>
          <text class="data-count">0<text class="unit">次</text></text>
        </view>
        <view class="data-item">
          <view class="data-icon club">🎟️</view>
          <text class="data-label">俱乐部</text>
          <text class="data-count">0<text class="unit">个</text></text>
        </view>
        <view class="data-item">
          <view class="data-icon timer">⏱️</view>
          <text class="data-label">累计时长</text>
          <text class="data-count">0<text class="unit">h</text></text>
        </view>
      </view>
    </view>
    
    <!-- 功能模块区 -->
    <view class="function-modules">
      <view class="module-item" v-for="(item, index) in modules" :key="index">
        <view class="module-icon" :class="item.iconClass">
          <text class="iconfont">{{ item.icon }}</text>
          <text class="badge" v-if="item.badge">{{ item.badge }}</text>
        </view>
        <text class="module-name">{{ item.name }}</text>
      </view>
    </view>
    
    <!-- 推广入驻区 -->
    <view class="promo-section">
      <view class="promo-item">
        <view class="promo-icon fire">🔥</view>
        <view class="promo-content">
          <text class="promo-title">我要推广</text>
          <text class="promo-desc">提高曝光</text>
        </view>
      </view>
      
      <view class="promo-item">
        <view class="promo-icon invite">✉️</view>
        <view class="promo-content">
          <text class="promo-title">邀请入驻</text>
          <text class="promo-desc">一起动起来</text>
        </view>
      </view>
      
      <view class="promo-item">
        <view class="promo-icon venue">🏬</view>
        <view class="promo-content">
          <text class="promo-title">场馆入驻</text>
          <text class="promo-desc">申请入驻平台</text>
        </view>
      </view>
    </view>
    
    <!-- 广告横幅 -->
    <view class="ad-banner">
      <view class="ad-content">
        <view class="ad-icon">📄</view>
        <view class="ad-text">
          <text class="ad-title">2025招行北京工</text>
          <text class="ad-subtitle">体育锻炼项目</text>
        </view>
      </view>
      <view class="ad-button">立即使用</view>
    </view>
    
    <!-- 底部导航 -->
    <view class="tab-bar">
      <view class="tab-item active">
        <text class="tab-icon">⚡</text>
        <text class="tab-name">闪动</text>
      </view>
      <view class="tab-item">
        <text class="tab-icon">🏠</text>
        <text class="tab-name">找场馆</text>
      </view>
      <view class="tab-item add-btn">
        <text class="add-icon">+</text>
      </view>
      <view class="tab-item">
        <text class="tab-icon">🏆</text>
        <text class="tab-name">俱乐部</text>
      </view>
      <view class="tab-item current">
        <text class="tab-icon">👤</text>
        <text class="tab-name">我的</text>
      </view>
    </view>
  </view>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue';

// 当前时间
const currentTime = ref('22:08');

// 更新时间函数
const updateTime = () => {
  const now = new Date();
  const hours = now.getHours().toString().padStart(2, '0');
  const minutes = now.getMinutes().toString().padStart(2, '0');
  currentTime.value = `${hours}:${minutes}`;
};

// 功能模块数据
const modules = ref([
  { icon: '📋', name: '我的订单', iconClass: 'order' },
  { icon: '💰', name: '我的钱包', iconClass: 'wallet' },
  { icon: '🎟️', name: '我的卡券', iconClass: 'coupon', badge: 'NEW' },
  { icon: '🔧', name: '工具箱', iconClass: 'tools' },
  { icon: '🔍', name: '活动', iconClass: 'activity' }
]);

// 定时器
let timer: number | null = null;

onMounted(() => {
  updateTime(); // 初始更新
  // 每分钟更新一次时间
  timer = setInterval(updateTime, 60000) as unknown as number;
});

onUnmounted(() => {
  if (timer) {
    clearInterval(timer);
  }
});
</script>

<style scoped>
.mine-container {
  position: relative;
  height: 100vh;
  background-color: #f5f5f5;
}

/* 渐变背景 */
.bg-gradient {
  background: linear-gradient(120deg, #fa9efc 0%, #a6c1ee 100%);
  padding-bottom: 150px;
  position: relative;
}

/* 状态栏 */
.status-bar {
  display: flex;
  justify-content: space-between;
  padding: 10px 20px;
  color: white;
}

.status-icons {
  display: flex;
  gap: 8px;
}

/* 头部控制区 */
.header-controls {
  display: flex;
  justify-content: space-between;
  padding: 10px 20px;
}

.left-controls, .right-controls {
  display: flex;
  gap: 20px;
}

.icon-btn {
  width: 40px;
  height: 40px;
  background-color: rgba(255, 255, 255, 0.2);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.more-btn {
  display: flex;
  align-items: center;
  background-color: rgba(255, 255, 255, 0.2);
  border-radius: 20px;
  padding: 0 20px;
  height: 40px;
}

.circle-btn {
  width: 40px;
  height: 40px;
  background-color: white;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  color: #555;
}

/* 横幅广告区 */
.banner-section {
  position: relative;
  height: 220px;
  margin-top: 20px;
  background: linear-gradient(135deg, #00c6ff, #0072ff);
  border-radius: 15px;
  margin: 20px;
  overflow: hidden;
}

.banner-content {
  position: absolute;
  top: 0;
  left: 0;
  padding: 20px;
  color: white;
}

.banner-title {
  font-size: 28px;
  font-weight: bold;
  margin-bottom: 10px;
  display: flex;
  align-items: center;
  gap: 10px;
}

.line1 {
  font-size: 32px;
}

.flash-x {
  font-size: 26px;
  color: #00ffcc;
}

.banner-subtitle {
  font-size: 32px;
  font-weight: bold;
  margin-bottom: 20px;
}

.banner-tags {
  display: flex;
  gap: 10px;
  margin-top: 30px;
}

.tag {
  padding: 5px 15px;
  border-radius: 20px;
  font-size: 14px;
}

.flash-tag {
  background-color: #ff66cc;
  color: white;
}

.come-on-tag {
  background-color: white;
  color: #333;
}

/* 用户信息卡片 */
.user-card {
  position: relative;
  margin: -100px 20px 20px;
  background-color: white;
  border-radius: 15px;
  padding: 20px;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.05);
}

.user-info {
  display: flex;
  align-items: center;
  gap: 15px;
}

.avatar {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  border: 3px solid #f0f0f0;
  background: linear-gradient(45deg, #6e8efb, #a777e3);
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  font-size: 36px;
  font-weight: bold;
}

.username {
  font-size: 18px;
  font-weight: bold;
  margin-bottom: 8px;
}

.edit-btn {
  display: inline-block;
  font-size: 14px;
  color: #999;
  border: 1px solid #ddd;
  border-radius: 15px;
  padding: 2px 10px;
}

.user-stats {
  margin-top: 10px;
  margin-left: 95px;
  font-size: 14px;
  color: #999;
}

/* 活动数据 */
.activity-data {
  display: flex;
  margin-top: 20px;
  border-top: 1px solid #f5f5f5;
  padding-top: 15px;
}

.data-item {
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.data-icon {
  margin-bottom: 5px;
  font-size: 24px;
}

.data-label {
  font-size: 14px;
  color: #999;
  margin-bottom: 5px;
}

.data-count {
  font-size: 24px;
  font-weight: bold;
  color: #333;
}

.unit {
  font-size: 14px;
  font-weight: normal;
  color: #999;
}

/* 功能模块区 */
.function-modules {
  display: flex;
  background-color: white;
  margin: 0 20px 20px;
  border-radius: 15px;
  padding: 20px 10px;
  justify-content: space-between;
}

.module-item {
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.module-icon {
  position: relative;
  width: 40px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 8px;
  font-size: 24px;
}

.badge {
  position: absolute;
  top: -5px;
  right: -5px;
  background-color: #ff3b30;
  color: white;
  font-size: 10px;
  padding: 2px 5px;
  border-radius: 10px;
}

.module-name {
  font-size: 14px;
  color: #333;
}

/* 图标颜色 */
.coupon .iconfont {
  color: #2196f3;
}

.wallet .iconfont {
  color: #00bcd4;
}

.order .iconfont {
  color: #4caf50;
}

.tools .iconfont {
  color: #ff9800;
}

.activity .iconfont {
  color: #9c27b0;
}

/* 推广入驻区 */
.promo-section {
  display: flex;
  gap: 15px;
  margin: 0 20px 20px;
}

.promo-item {
  flex: 1;
  background-color: white;
  border-radius: 15px;
  padding: 15px;
  display: flex;
  align-items: center;
  gap: 10px;
}

.promo-icon {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 20px;
}

.fire {
  background-color: #ffecee;
  color: #ff4d6a;
}

.invite {
  background-color: #e8f5fe;
  color: #0099ff;
}

.venue {
  background-color: #f1e7fc;
  color: #9966ff;
}

.promo-content {
  display: flex;
  flex-direction: column;
  flex: 1;
}

.promo-title {
  font-size: 14px;
  font-weight: bold;
  margin-bottom: 3px;
}

.promo-desc {
  font-size: 12px;
  color: #999;
}

/* 广告横幅 */
.ad-banner {
  margin: 0 20px 20px;
  background: linear-gradient(90deg, #ff6b6b, #ff9d66);
  border-radius: 15px;
  padding: 15px 20px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  color: white;
}

.ad-content {
  display: flex;
  align-items: center;
  gap: 10px;
}

.ad-icon {
  font-size: 24px;
}

.ad-text {
  display: flex;
  flex-direction: column;
}

.ad-title {
  font-size: 16px;
  font-weight: bold;
}

.ad-subtitle {
  font-size: 14px;
}

.ad-button {
  background-color: #ffdd59;
  color: #333;
  padding: 8px 15px;
  border-radius: 20px;
  font-size: 14px;
  font-weight: bold;
}

/* 底部导航 */
.tab-bar {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  height: 60px;
  background-color: white;
  display: flex;
  align-items: center;
  box-shadow: 0 -2px 10px rgba(0, 0, 0, 0.05);
}

.tab-item {
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  color: #999;
}

.tab-icon {
  font-size: 20px;
  margin-bottom: 3px;
}

.tab-name {
  font-size: 12px;
}

.add-btn {
  height: 50px;
  width: 50px;
  background-color: #00deff;
  border-radius: 50%;
  margin-top: -20px;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 2px 10px rgba(0, 221, 255, 0.3);
}

.add-icon {
  font-size: 30px;
  color: white;
}

.active {
  color: #00deff;
}

.current {
  color: #333;
}
</style> 