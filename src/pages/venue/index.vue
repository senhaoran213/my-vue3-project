<template>
  <view class="venue-container">
    <!-- 顶部导航栏 -->
    <wd-navbar custom-title>
      <template #center>
        <view class="nav-title">
          <view class="nav-item active">约场馆</view>
          <view class="nav-item">购门票</view>
        </view>
      </template>
      <template #right>
        <view class="nav-icons">
          <wd-icon name="more" size="22px" color="#333"></wd-icon>
          <wd-icon name="search" size="22px" color="#333" class="search-icon"></wd-icon>
        </view>
      </template>
    </wd-navbar>

    <!-- 活动广告横幅 -->
    <wd-card custom-class="banner-card">
      <view class="banner">
        <view class="banner-content">
          <view class="banner-left">
            <view class="banner-title">
              <text class="title-main">9</text>
              <text class="title-sub">8</text>
              <view class="banner-eyes">
                <image src="/static/images/venue/eyes.png" mode="widthFix" class="eyes-img"></image>
              </view>
            </view>
            <view class="banner-desc">7</view>
            <view class="search-box">
              <wd-icon name="search" size="16px" color="#999"></wd-icon>
              <text class="search-text">场馆名称</text>
            </view>
          </view>
          <view class="banner-right">
            <view class="right-item">6</view>
            <view class="right-item">5</view>
            <view class="right-item">4</view>
            <view class="right-item">3</view>
            <view class="right-btn">2 >>></view>
            <view class="recommend-btn">
              <wd-icon name="fire" size="16px" color="#fff"></wd-icon>
              <text>1</text>
            </view>
          </view>
        </view>
      </view>
    </wd-card>

    <!-- 分类标签 -->
    <view class="category-tabs">
      <scroll-view scroll-x class="category-scroll">
        <view class="category-list">
          <view 
            v-for="(category, index) in categories" 
            :key="index" 
            class="category-item" 
            :class="{ active: currentCategory === category.id }"
            @click="changeCategory(category.id)"
          >
            <view class="category-icon">{{ category.icon }}</view>
            <text class="category-text">{{ category.name }}</text>
          </view>
        </view>
      </scroll-view>
    </view>

    <!-- 筛选条件 -->
    <wd-cell-group custom-class="filter-group">
      <view class="filter-bar">
        <view class="filter-item" @click="toggleFilter('popularity')">
          <text>{{ filters.popularity.options[filters.popularity.current] }}</text>
          <wd-icon name="arrow-down" size="12px" color="#666"></wd-icon>
        </view>
        <view class="filter-item" @click="toggleFilter('area')">
          <text>{{ filters.area.options[filters.area.current] }}</text>
          <wd-icon name="arrow-down" size="12px" color="#666"></wd-icon>
        </view>
        <view class="filter-item" @click="toggleFilter('city')">
          <text>{{ filters.city.options[filters.city.current] }}</text>
          <wd-icon name="arrow-down" size="12px" color="#666"></wd-icon>
        </view>
      </view>
    </wd-cell-group>

    <!-- 场馆列表 -->
    <view v-if="filteredVenueList.length > 0" class="venue-list">
      <wd-card v-for="(venue, index) in filteredVenueList" :key="index" custom-class="venue-card">
        <view class="venue-item">
          <view class="venue-image">
            <wd-img :src="venue.image" width="170" height="120" custom-class="venue-img" round></wd-img>
            <view v-if="venue.badge" class="venue-badge">{{ venue.badge }}</view>
          </view>
          <view class="venue-info">
            <view class="venue-name">{{ venue.name }}</view>
            <view class="venue-tags">
              <view v-for="(tag, tagIndex) in venue.tags" :key="tagIndex" class="venue-tag">
                {{ tag }}
              </view>
            </view>
            <view class="venue-address">
              <wd-icon name="location" size="14px" color="#999"></wd-icon>
              <text>{{ venue.address }}</text>
            </view>
            <view class="venue-price">
              <text class="price">¥{{ venue.price }}</text>
              <text class="unit">/次起</text>
              <view class="distance">{{ venue.distance }}km</view>
            </view>
          </view>
        </view>
      </wd-card>
    </view>

    <!-- 场馆列表 - 无数据状态 -->
    <view v-else class="venue-list-empty">
      <wd-img src="/static/images/venue/empty.png" width="160" height="160" custom-class="empty-img" fill="contain"></wd-img>
      <text class="empty-text">暂无场馆</text>
      <text class="empty-desc">到底啦</text>
    </view>

    <!-- 底部小店入口 -->
    <view class="shop-entry">
      <wd-badge value="1">
        <wd-img src="/static/images/venue/shop.png" width="100" height="100" custom-class="shop-img" fill="contain"></wd-img>
      </wd-badge>
    </view>

    <!-- 筛选弹窗 -->
    <wd-action-sheet
      v-model="actionSheetVisible"
      :actions="currentFilterOptions"
      title="请选择"
      @select="handleFilterSelect"
    ></wd-action-sheet>

    <!-- TabBar占位 -->
    <view class="tabbar-placeholder"></view>
  </view>
</template>

<script setup lang="ts">
import { ref, reactive, computed } from 'vue';

// 定义类型
interface Category {
  id: string;
  name: string;
  icon: string;
}

interface FilterOption {
  name: string;
  options: string[];
  current: number;
}

interface Filters {
  popularity: FilterOption;
  area: FilterOption;
  city: FilterOption;
  [key: string]: FilterOption;
}

interface Venue {
  id: number;
  categoryId: string;
  name: string;
  image: string;
  tags: string[];
  address: string;
  price: number;
  distance: number;
  popularity: number;
  areaId: number;
  cityId: number;
  badge: string | null;
}

interface ActionItem {
  name: string;
  value: number;
}

// 分类数据
const categories = reactive<Category[]>([
  { id: 'recommend', name: '推荐', icon: '👍' },
  { id: 'ice', name: '冰上运动', icon: '🏊' },
  { id: 'boat', name: '船艇运动', icon: '🚢' },
  { id: 'outdoor', name: '户外运动', icon: '🏕️' },
  { id: 'ball', name: '球类运动', icon: '⚽' },
  { id: 'fitness', name: '健身', icon: '💪' },
]);

// 当前选中分类
const currentCategory = ref<string>('recommend');

// 筛选条件
const filters = reactive<Filters>({
  popularity: {
    name: 'popularity',
    options: ['人气最高', '评分最高', '价格最低', '价格最高'],
    current: 0
  },
  area: {
    name: 'area',
    options: ['全城', '附近5km', '附近10km'],
    current: 0
  },
  city: {
    name: 'city',
    options: ['福州', '厦门', '泉州', '漳州'],
    current: 0
  }
});

// 场馆数据
const venueList = reactive<Venue[]>([
  // 推荐场馆
  {
    id: 1,
    categoryId: 'recommend',
    name: '风动体育馆',
    image: '/static/images/venue/venue1.png',
    tags: ['足球', '篮球', '羽毛球'],
    address: '仓山区金山大道618号',
    price: 88,
    distance: 2.5,
    popularity: 98,
    areaId: 0,
    cityId: 0,
    badge: '热门'
  },
  {
    id: 2,
    categoryId: 'recommend',
    name: '华大体育中心',
    image: '/static/images/venue/venue2.png',
    tags: ['篮球', '排球'],
    address: '大学城学园路2号',
    price: 65,
    distance: 3.7,
    popularity: 92,
    areaId: 0,
    cityId: 0,
    badge: null
  },
  {
    id: 3,
    categoryId: 'ice',
    name: '冰纷万象滑冰场',
    image: '/static/images/venue/venue3.png',
    tags: ['滑冰', '冰壶'],
    address: '台江区台江路88号',
    price: 120,
    distance: 5.2,
    popularity: 95,
    areaId: 1,
    cityId: 0,
    badge: '新店'
  },
  {
    id: 4,
    categoryId: 'boat',
    name: '闽江皮划艇基地',
    image: '/static/images/venue/venue4.png',
    tags: ['皮划艇', '划船'],
    address: '仓山区闽江大道108号',
    price: 150,
    distance: 7.8,
    popularity: 88,
    areaId: 1,
    cityId: 0,
    badge: null
  },
  {
    id: 5,
    categoryId: 'outdoor',
    name: '鼓山登山营地',
    image: '/static/images/venue/venue5.png',
    tags: ['登山', '露营'],
    address: '鼓楼区鼓山路66号',
    price: 45,
    distance: 10.5,
    popularity: 90,
    areaId: 2,
    cityId: 0,
    badge: '优惠'
  },
  {
    id: 6,
    categoryId: 'ball',
    name: '全明星羽毛球馆',
    image: '/static/images/venue/venue6.png',
    tags: ['羽毛球', '乒乓球'],
    address: '晋安区岳峰镇福新东路96号',
    price: 75,
    distance: 4.3,
    popularity: 94,
    areaId: 0,
    cityId: 0,
    badge: null
  },
  {
    id: 7,
    categoryId: 'fitness',
    name: '超级健身会所',
    image: '/static/images/venue/venue7.png',
    tags: ['健身', '瑜伽'],
    address: '鼓楼区五四路128号',
    price: 98,
    distance: 1.8,
    popularity: 96,
    areaId: 0,
    cityId: 0,
    badge: '推荐'
  }
]);

// 弹窗相关
const actionSheetVisible = ref<boolean>(false);
const currentFilterType = ref<string>('');
const currentFilterOptions = ref<ActionItem[]>([]);

// 切换分类
const changeCategory = (categoryId: string): void => {
  currentCategory.value = categoryId;
};

// 切换筛选条件
const toggleFilter = (filterType: string): void => {
  currentFilterType.value = filterType;
  currentFilterOptions.value = filters[filterType].options.map((option: string, index: number) => ({
    name: option,
    value: index
  }));
  actionSheetVisible.value = true;
};

// 处理筛选选择
const handleFilterSelect = (item: ActionItem): void => {
  filters[currentFilterType.value].current = item.value;
  actionSheetVisible.value = false;
};

// 筛选场馆列表
const filteredVenueList = computed<Venue[]>(() => {
  let result = venueList.filter(venue => {
    // 根据当前分类筛选
    if (currentCategory.value !== 'recommend' && venue.categoryId !== currentCategory.value) {
      return false;
    }
    
    // 根据区域筛选
    if (filters.area.current !== 0 && venue.areaId !== filters.area.current) {
      return false;
    }
    
    // 根据城市筛选
    if (filters.city.current !== 0 && venue.cityId !== filters.city.current) {
      return false;
    }
    
    return true;
  });
  
  // 根据人气/价格排序
  if (filters.popularity.current === 0) {
    // 人气最高
    result.sort((a, b) => b.popularity - a.popularity);
  } else if (filters.popularity.current === 1) {
    // 评分最高（模拟评分为0-100）
    result.sort((a, b) => b.popularity - a.popularity);
  } else if (filters.popularity.current === 2) {
    // 价格最低
    result.sort((a, b) => a.price - b.price);
  } else if (filters.popularity.current === 3) {
    // 价格最高
    result.sort((a, b) => b.price - a.price);
  }
  
  return result;
});
</script>

<style lang="scss" scoped>
.venue-container {
  min-height: 100vh;
  background-color: #f5f5f5;
  padding-bottom: 120rpx;
}

/* 顶部导航栏 */
:deep(.wd-navbar) {
  background-color: #fff;
  
  .nav-title {
    display: flex;
    align-items: center;
    
    .nav-item {
      font-size: 32rpx;
      padding: 0 20rpx;
      position: relative;
      
      &.active {
        font-weight: bold;
        
        &::after {
          content: '';
          position: absolute;
          bottom: -10rpx;
          left: 50%;
          transform: translateX(-50%);
          width: 40rpx;
          height: 4rpx;
          background-color: #000;
          border-radius: 2rpx;
        }
      }
    }
  }

  .nav-icons {
    display: flex;
    align-items: center;
    
    .search-icon {
      margin-left: 20rpx;
    }
  }
}

/* 活动广告横幅 */
:deep(.banner-card) {
  margin: 20rpx;
  border-radius: 20rpx !important;
  overflow: hidden;
  padding: 0 !important;
}

.banner {
  background: linear-gradient(135deg, #ffd500, #75eeff);
  
  .banner-content {
    display: flex;
    padding: 30rpx;
    
    .banner-left {
      flex: 3;
      
      .banner-title {
        position: relative;
        margin-bottom: 20rpx;
        
        .title-main {
          font-size: 48rpx;
          font-weight: bold;
          color: #000;
          line-height: 1.2;
          display: block;
        }
        
        .title-sub {
          font-size: 48rpx;
          font-weight: bold;
          color: #28ce26;
          line-height: 1.2;
          display: block;
        }

        .banner-eyes {
          position: absolute;
          top: 10rpx;
          right: 20%;
          
          .eyes-img {
            width: 60rpx;
          }
        }
      }
      
      .banner-desc {
        font-size: 24rpx;
        color: #333;
        margin-bottom: 30rpx;
      }
      
      .search-box {
        display: flex;
        align-items: center;
        background-color: rgba(255, 255, 255, 0.8);
        padding: 12rpx 20rpx;
        border-radius: 30rpx;
        width: 80%;
        
        .search-text {
          margin-left: 10rpx;
          font-size: 24rpx;
          color: #999;
        }
      }
    }
    
    .banner-right {
      flex: 2;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      
      .right-item {
        background-color: rgba(255, 255, 255, 0.7);
        padding: 8rpx 16rpx;
        border-radius: 10rpx;
        font-size: 22rpx;
        margin-bottom: 10rpx;
        color: #333;
      }
      
      .right-btn {
        background-color: rgba(0, 0, 0, 0.7);
        color: #fff;
        text-align: center;
        padding: 10rpx;
        border-radius: 10rpx;
        font-size: 24rpx;
        margin-top: 10rpx;
      }

      .recommend-btn {
        background-color: #ff5a5a;
        color: #fff;
        display: flex;
        align-items: center;
        justify-content: center;
        padding: 10rpx;
        border-radius: 10rpx;
        font-size: 24rpx;
        margin-top: 10rpx;
        
        text {
          margin-left: 6rpx;
        }
      }
    }
  }
}

/* 分类标签 */
.category-tabs {
  margin: 20rpx 0;
  background-color: #fff;
  padding: 20rpx 0;
  
  .category-scroll {
    white-space: nowrap;
  }
  
  .category-list {
    display: flex;
    padding: 0 20rpx;
    
    .category-item {
      display: inline-flex;
      flex-direction: column;
      align-items: center;
      margin-right: 40rpx;
      
      &.active {
        .category-text {
          color: #00deff;
        }
      }
      
      .category-icon {
        font-size: 40rpx;
        margin-bottom: 10rpx;
      }
      
      .category-text {
        font-size: 24rpx;
        color: #666;
      }
    }
  }
}

/* 筛选条件 */
:deep(.filter-group) {
  margin: 0;
}

.filter-bar {
  display: flex;
  background-color: #fff;
  padding: 20rpx 30rpx;
  
  .filter-item {
    display: flex;
    align-items: center;
    margin-right: 40rpx;
    font-size: 26rpx;
    color: #666;
    
    text {
      margin-right: 4rpx;
    }
  }
}

/* 场馆列表 */
.venue-list {
  padding: 20rpx;
  display: flex;
  flex-direction: column;
  
  :deep(.venue-card) {
    margin-bottom: 20rpx;
    border-radius: 16rpx !important;
    overflow: hidden;
  }
  
  .venue-item {
    display: flex;
    
    .venue-image {
      position: relative;
      margin-right: 20rpx;
      
      .venue-badge {
        position: absolute;
        top: 10rpx;
        left: 10rpx;
        background-color: #ff5a5a;
        color: #fff;
        font-size: 22rpx;
        padding: 4rpx 10rpx;
        border-radius: 16rpx;
      }
    }
    
    .venue-info {
      flex: 1;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      
      .venue-name {
        font-size: 32rpx;
        font-weight: bold;
        margin-bottom: 10rpx;
        color: #333;
      }
      
      .venue-tags {
        display: flex;
        flex-wrap: wrap;
        margin-bottom: 10rpx;
        
        .venue-tag {
          background-color: #f5f5f5;
          color: #666;
          font-size: 22rpx;
          padding: 4rpx 12rpx;
          border-radius: 10rpx;
          margin-right: 10rpx;
          margin-bottom: 8rpx;
        }
      }
      
      .venue-address {
        display: flex;
        align-items: center;
        font-size: 24rpx;
        color: #999;
        margin-bottom: 10rpx;
        
        text {
          margin-left: 6rpx;
        }
      }
      
      .venue-price {
        display: flex;
        align-items: baseline;
        
        .price {
          font-size: 34rpx;
          font-weight: bold;
          color: #ff5a5a;
        }
        
        .unit {
          font-size: 24rpx;
          color: #999;
          margin-left: 4rpx;
        }
        
        .distance {
          margin-left: auto;
          color: #999;
          font-size: 24rpx;
        }
      }
    }
  }
}

/* 场馆列表 - 无数据状态 */
.venue-list-empty {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 100rpx 0;
  
  :deep(.empty-img) {
    opacity: 0.6;
    margin-bottom: 20rpx;
  }
  
  .empty-text {
    font-size: 30rpx;
    color: #999;
    margin-bottom: 10rpx;
  }
  
  .empty-desc {
    font-size: 24rpx;
    color: #ccc;
  }
}

/* 底部小店入口 */
.shop-entry {
  position: fixed;
  right: 30rpx;
  bottom: 160rpx;
}

/* TabBar占位 */
.tabbar-placeholder {
  height: 100rpx;
}
</style> 