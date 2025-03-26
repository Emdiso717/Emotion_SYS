<template>
  <div class="foresight-container card-large">
    <h2>法律证据链</h2>
    <div class="foresight-grid">
      <div class="row">
        <div class="detail-result-card">
          <div class="detail-result-title">结果详情</div>
          <div class="detail-result-content">
            <p>{{ data.detailresult }}</p>
          </div>
        </div>
        <!-- 按钮容器 -->
        <div class="button-container">
          <button class="action-button-1">
            <span class="button-text">获取法律建议</span>
            <font-awesome-icon :icon="['fas', 'arrow-right']" class="icon-arrowright"/>
          </button>
          <button class="action-button-2">
            <span class="button-text">导出评论</span>
            <font-awesome-icon :icon="['fas', 'arrow-right']" class="icon-arrowright"/>
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    data: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style scoped>
/* 主容器样式 */
.foresight-container {
  flex: 1;
  display: flex;
  flex-direction: column;
  padding: 1rem;
}

.foresight-grid {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  flex: 1;
}

.row {
  display: flex;
  gap: 2rem;
  flex: 1;
  margin-left: 1.5rem;
  margin-right: 1.5rem;
}

.detail-result-card {
  flex: 1;
  display: flex;
  flex-direction: column;
  background: linear-gradient(to bottom, #eef8ff, white);
  border-radius: 8px;
  padding: 1rem;
  position: relative; /* 为遮罩定位做准备 */
  overflow: hidden; /* 防止遮罩溢出 */
  max-height: 320px;
}

.detail-result-title {
  text-align: center;
  font-size: 24px;
  font-weight: bold;
  color: #333;
  margin-bottom: 1rem;
  padding-bottom: 1rem;
  align-self: center;
  font-family: Microsoft JhengHei UI;
  border-bottom: 1px solid #ddd;
  width: 90%;
  letter-spacing: 5px;
}

.detail-result-content {
  flex: 1;
  padding: 1rem 0;
  overflow-y: auto; /* 内容过多时启用滚动 */
  position: relative; /* 为遮罩定位做准备 */
}

/* 渐变遮罩 */
.detail-result-card::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 60px; /* 遮罩高度 */
  background: linear-gradient(to bottom, rgba(238, 248, 255, 0), #eef8ff); /* 从透明到背景色 */
  pointer-events: none; /* 防止遮罩阻挡交互 */
}

.detail-result-content::-webkit-scrollbar {
  width: 2px; /* 滚动条宽度 */
}

.detail-result-content::-webkit-scrollbar-track {
  background: transparent; /* 滚动条轨道背景 */
  border-radius: 4px;
}

.detail-result-content::-webkit-scrollbar-thumb {
  background: #146AF466; /* 滚动条滑块颜色 */
  border-radius: 1px;
}

.detail-result-content::-webkit-scrollbar-thumb:hover {
  background: #146AF488; /* 滚动条滑块悬停颜色 */
}

.detail-result-content p {
  margin-left: 5%;
  margin-right: 5%;
  color: #000000;
  font-size: 16px;
}

/* 按钮容器样式 */
.button-container {
  display: flex;
  flex-direction: column;
  gap: 1rem; /* 按钮之间的间距 */
  justify-content: center; /* 垂直居中 */
  width: 200px; /* 按钮容器宽度 */
  height: 100%; /* 高度填满父容器 */
}

/* 按钮样式 */
.action-button-1,
.action-button-2 {
  display: flex;
  align-items: center; /* 垂直居中 */
  justify-content: space-between; /* 文字和图标分别靠左和靠右 */
  background: #E9E9E9; /* 按钮背景色 */
  color: #000000; /* 按钮文字颜色 */
  border: 1px solid #8F8F8F;
  border-radius: 50px;
  padding: 1rem;
  font-size: 20px;
  font-weight: 400;
  font-family: Microsoft JhengHei UI;
  cursor: pointer;
  transition: background 0.3s ease;
}

.action-button-1:hover {
  background: #d0d0d0; 
}

.action-button-2 {
  background: #5484D1; 
  color: white; 
  border: 1px solid #E0E0E0;
}

.action-button-2:hover {
  background: #0056b3; 
}

/* 按钮文字样式 */
.button-text {
  flex: 1; /* 文字占据剩余空间 */
  text-align: center; /* 文字居中 */
  font-size: 18px;
}

/* 图标样式 */
.icon-arrowright {
  font-size: 20px;
  margin-left: auto; /* 将图标推到右侧 */
}

/* 标题样式 */
h2 {
  margin: 0 0 1rem 1.5rem;
  font-size: 36px;
  color: #333;
  font-family: Microsoft JhengHei UI;
  letter-spacing: 7px;
}

h3 {
  margin: 0 0 0.75rem 0;
  font-size: 32px;
  color: #000000;
  font-family: Microsoft JhengHei UI;
  letter-spacing: 8px;
}

p {
  font-size: 18px;
  color: #000000;
  font-weight: 400;
  letter-spacing: 1px;
  line-height: 150%;
  white-space: pre-line;
}
</style>