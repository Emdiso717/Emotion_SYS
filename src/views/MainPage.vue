<template>
  <div class="app-container">
    <Sidebar :products="products" @product-selected="loadProductData" />
    <div class="main-content">

      <div class="header-container">
        <Header @search="handleSearch" @filter="handleFilter" />
      </div>
      
      <div class="content-container">
        <WarningList :warnings="currentWarnings" />
      </div>
      
      <div class="footer-container">
        <Footer :stats="footerStats" />
      </div>
    </div>
  </div>
</template>


<script setup>
import { ref, onMounted } from 'vue'
import axios from 'axios'
import Header from '../components/MainPage/MainHeader.vue'
import Sidebar from '../components/MainPage/MainSidebar.vue'
import Footer from '../components/MainPage/MainFooter.vue'
import WarningList from '../components/MainPage/WarningList.vue'

const products = ref([])
const currentWarnings = ref([])
const lastMonthWarnings = ref([])
const footerStats = ref([])
const footerChanges = ref({})

onMounted(async () => {
  // 初始化加载产品数据
  const prodRes = await axios.get('/data/Production.json')
  products.value = prodRes.data.products
  if (products.value.length > 0) {
    loadProductData(products.value[0].id)
  }
})

// 加载产品警告数据
const loadProductData = async (productId) => {
  try {
    const warnRes = await axios.get(`/data/Pro_${productId}.json`)
    currentWarnings.value = warnRes.data.warnings
    
    updateFooterStats()
  } catch (error) {
    console.error('加载产品数据失败:', error)
    currentWarnings.value = []
  }
}

// 更新底部统计
const updateFooterStats = () => {
  const stats = {
    total: 0,
    high: 0,
    medium: 0,
    low: 0
  }
  
  currentWarnings.value.forEach(w => {
    stats.total++
    stats[w.priority.toLowerCase()]++
  })
  
  footerStats.value = stats
}
</script>

<style scoped>
/* 基础样式重置 */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: system-ui, -apple-system, sans-serif;
}

.app-container {
  min-height: 100vh;
  display: flex;
  background: #f5f6fa;
}

.main-content {
  flex: 1;
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

.header-container {
  flex-shrink: 0;
  position: sticky;
  top: 0;
  z-index: 100;
}

.content-container {
  flex-grow: 1;
  overflow-y: auto;
  padding: 15px;
}

.footer-container {
  flex-shrink: 0;
}

@media (max-width: 768px) {
  .app-container {
    flex-direction: column;
  }

  .content-container {
    min-height: calc(100vh - 120px); /* 根据实际header/footer高度调整 */
  }
}
</style>