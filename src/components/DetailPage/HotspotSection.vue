<template>
  <div class="hotspot-container card-large">
    <div class="hotspot-grid">
      <!-- 第一栏：信息流图 -->
      <div class="main-column">
        <h2>热点追踪</h2>
        <div class="card image-card">
          <h3>信息流图</h3>
          <InfomationFlow :If_id="data.fileName" />
        </div>
      </div>

      <!-- 第二栏：信息流解读、热点时间范围、词云 -->
      <div class="side-column">
        <div class="sub-row">
          <div class="card info-flow">
            <h4 class="info-flow-title">信息流图解读</h4>
            <p class="info-flow-content">{{ data.infoFlowInterpretation }}</p>
            <p class="click-more">点击查看更多 ...</p>
          </div>
          <div class="card time-range">
            <h4 class="time-range-title">热点时间范围</h4>
            <p class="time-range-content">{{ data.hotspotTimeRange }}</p>
          </div>
          <div class="card word-cloud">
            <h4 class="word-cloud-title">词云</h4>
            <div class="image-placeholder"><img alt="word" src="../../../public/word.png" /></div>
          </div>
        </div>

        <!-- 第二行：转折点分析和指标 -->
        <div class="sub-row">
          <div class="card turning-point">
            <h4 class="turning-point-title">转折点分析</h4>
            <p class="turning-point-content">{{ data.turningPointAnalysis }}</p>
            <p class="click-more">点击查看更多 ...</p>
          </div>
          <div class="metrics-grid">
            <!-- 手动编写每个指标卡片 -->
            <div class="card">
              <h4 class="metrics-grid-title">相关评论数</h4>
              <p class="metrics-grid-1">{{ data.relatedCommentsCount }}</p>
            </div>
            <div class="card">
              <h4 class="metrics-grid-title">平台数</h4>
              <p class="metrics-grid-2">{{ data.platformCount }}</p>
            </div>
            <div class="card">
              <h4 class="metrics-grid-title">最多评论来源</h4>
              <p class="metrics-grid-3">{{ data.mostCommentsSource }}</p>
            </div>
            <div class="card">
              <h4 class="metrics-grid-title">单平台最多评论</h4>
              <p class="metrics-grid-4">{{ data.singlePlatformMostComments }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import InfomationFlow from '../Public/InfomationFlow.vue'

export default {
  props: {
    data: {
      type: Object,
      required: true,
    },
  },
  components: {
    InfomationFlow
  }
};
</script>

<style scoped>
.hotspot-container {
  flex: 1;
}

.hotspot-grid {
  display: flex;
  gap: 2rem;
  /* 增加主栏与侧栏的间距 */
  height: 500px;
}

.main-column {
  flex: 1;
}

.side-column {
  flex: 2;
  display: flex;
  flex-direction: column;
  gap: 2rem;
  /* 增加侧栏内部的间距 */
}

.sub-row {
  display: flex;
  gap: 1.5rem;
  /* 增加子行内卡片的间距 */
  height: 50%;
}

.sub-row>.info-flow {
  flex: 3;
  /* 默认比例 */
}

.sub-row>.time-range {
  flex: 1;
  /* 占据两倍于默认比例的空间 */
}

.sub-row>.word-cloud {
  flex: 1.5;
  /* 占据1.5倍于默认比例的空间 */
}

.sub-row>.turning-point {
  flex: 1;
  /* 默认比例 */
}

.sub-row>.metrics-grid {
  flex: 1;
  /* 占据三倍于默认比例的空间 */
}

.metrics-grid {
  display: flex;
  flex-wrap: wrap;
  gap: 1.1rem;
  /* 增加指标卡片的间距 */
}

.metrics-grid>* {
  flex: 1 1 calc(50% - 0.75rem);
  /* 确保两列布局 */
  height: calc(50% - 0.75rem);
}

.card {
  background: white;
  border: 1px solid #ddd;
  border-radius: 8px;
  padding: 1.5rem;
  /* 增加卡片内边距 */
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  /* 增加阴影 */
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

h2 {
  margin: 0 0 1.5rem 0;
  /* 增加标题与内容的间距 */
  font-size: 36px;
  color: #333;
  font-family: Microsoft JhengHei UI;
}

h3 {
  margin: 0 0 0.75rem 0;
  /* 增加小标题与内容的间距 */
  font-size: 32px;
  color: #000000;
  font-family: Microsoft JhengHei UI;
}

h4 {
  margin: 0 0 0.75rem 0;
  /* 增加小标题与内容的间距 */
  font-size: 1.1rem;
  color: #555;
}

p {
  margin: 0;
  color: #777;
}

.image-card {
  display: flex;
  flex-direction: column;
  width: 100%;
  height: calc(100% - 4.35rem);

}

.image-placeholder {
  width: 100%;
  height: 100%;
  background: #ffffff;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 4px;
}

.info-flow-title {
  font-size: 24px;
  font-family: Microsoft JhengHei UI;
}

.info-flow-content {
  flex-grow: 1;
  font-size: 16px;
  line-height: 150%;
  white-space: pre-line;
  font-family: OPlusSans 3.0;
}

.time-range-title {
  font-size: 24px;
  text-align: center;
  /* 热点时间范围标题居中 */
  font-family: Microsoft JhengHei UI;
}

.time-range-content {
  display: flex;
  flex-direction: column;
  align-items: center;
  /* 热点时间范围内容居中 */
  justify-content: center;
  text-align: center;
  height: 100%;
  font-size: 20px;
  font-weight: 600;
  white-space: pre-line;
}

.word-cloud-title {
  font-size: 26px;
  letter-spacing: 4%;
  text-align: center;
  /* 词云标题居中 */
  font-family: Microsoft JhengHei UI;
}

.word-cloud-image {
  width: 100%;
  height: auto;
  border-radius: 4px;
}

.turning-point-title {
  text-transform: uppercase;
  font-size: 24px;
  text-align: center;
  font-family: Microsoft JhengHei UI;
}

.turning-point-content {
  flex-grow: 1;
  font-size: 16px;
  line-height: 150%;
  line-height: 136%;
}

.click-more {
  text-align: center;
  color: #828282;
  cursor: pointer;
  margin-top: 0.5rem;
  font-size: 14px;
}

.metric {
  font-family: 'Trebuchet MS', sans-serif;
  color: #1467EB;
}

/* 单独设置每个指标卡片的颜色 */
.metrics-grid-title {
  font-size: 15px;
  color: #000000;
  font-weight: 500;
}

.metrics-grid-1 {
  font-size: 24px;
  color: #1467EB;
  font-weight: 600;
}

.metrics-grid-2 {
  font-size: 24px;
  color: #88C3FF;
  font-weight: 600;
}

.metrics-grid-3 {
  font-size: 24px;
  color: #828282;
  font-weight: 500;
}

.metrics-grid-4 {
  font-size: 24px;
  color: #828282;
  font-weight: 600;
}
</style>