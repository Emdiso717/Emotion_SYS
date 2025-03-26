<template>
  <div class="sidebar-container">
    <div class="sidebar-card">
      <h2 class="title">企业产品</h2>
      <div class="product-scroll">
        <ProductItem
          v-for="product in products"
          :key="product.id"
          :product="product"
          :isActive="selectedProduct === product.id"
          @select="selectProduct"
        />
        <button class="add-button">
        <font-awesome-icon icon="plus" />
      </button>
      </div>
      
      
      <div class="total-card">
  <span class="label">产品</span>
  <span class="sub-label">总数 Total</span>
  <span class="value">{{ products.length }}</span>
</div>
    </div>
  </div>
</template>

<script setup>
import { ref,onMounted,defineEmits} from 'vue'
import ProductItem from './ProductItem.vue'

// 定义响应式数据
const products = ref([])
const selectedProduct = ref(null)

// 加载 JSON 数据
onMounted(async () => {
  try {
    const response = await fetch('/data/Production.json')
    console.log('Response status:', response.status) // 打印状态码
    if (!response.ok) {
      throw new Error('Failed to load data')
    }
    const data = await response.json()
    console.log('Loaded data:', data) // 打印加载的数据
    products.value = data.products // 提取 products 数组
  } catch (error) {
    console.error('Error loading data:', error)
  }
})

const emit = defineEmits(['select-selected'])
// 选择产品

const selectProduct = (productId) => {
  selectedProduct.value = productId
  emit('product-selected', productId)
}
</script>

<style scoped>
.sidebar-container {
  padding-left:10px;
  padding-top:10px;
  padding-bottom:20px;
  width: 15%;
  min-height: calc(100vh - 200px); /* 计算可用高度 */
}

.sidebar-card {
  background: white;
  border-radius: 16px;
  padding: 0px;
  height: 100%;
  display: flex;
  flex-direction: column;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

.title {
  margin-top: 40px;
  text-align: center;
  margin-bottom: 20px;
  font-size: 2.5em;
  color: #333;
  font-family: PangMenZhengDao;
}

.product-scroll {
  flex: 1;
  margin: 15px 0;
  overflow-y: auto;
}

.product-scroll > * {
  margin-bottom: 5px; /* 调整 ProductItem 之间的间距 */
}

.add-button {
  background: linear-gradient(45deg, #146AF4, #88C3FF); 
  color: white;
  padding: 16px; 
  border-radius: 50%; 
  width: 40px; 
  height: 40px; 
  display: flex;
  align-items: center;
  justify-content: center; 
  text-align: center;
  font-size: 0.9em;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2); 
  margin: 20px auto; 
  cursor: pointer; 
  border: none; 
  outline: none; 
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.add-button:hover {
  animation: pulse 0.5s ease-in-out infinite alternate; /* 悬停时播放动画 */
}

@keyframes pulse {
  0% {
    transform: scale(1);
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);
  }
  100% {
    transform: scale(1.05);
    box-shadow: 0 6px 16px rgba(0, 0, 0, 0.3);
  }
}
.total-card {
  background: linear-gradient(45deg, #146AF4, #88C3FF); 
  color: white;
  padding: 16px;
  border-radius: 8px;
  margin: 20px; 
  text-align: center;
  font-size: 0.9em;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2); 
  display: flex;
  flex-direction: column;
  gap: 8px; 
  height: 15%;
  text-align: left;
  box-shadow: inset -2px 2px 10px 2px #FFFFFF80;
}

.total-card .label {
  font-size: 14px; 
  font-weight: 500;
  text-shadow: 2px 4px 4px rgba(0, 0, 0, 0.3); 
  margin-left: 10px;
  font-family: OPlusSans 3.0;
}

.total-card .sub-label {
  font-size: 14px; 
  font-weight: 400;
  text-shadow: 2px 4px 4px rgba(0, 0, 0, 0.3); 
  margin-left: 10px;
  font-family: OPlusSans 3.0;
}

.total-card .value {
  font-size: 48px; 
  font-weight: 700;
  text-shadow: 2px 4px 4px rgba(0, 0, 0, 0.3); 
  margin-left: 10px;
  align-items: flex-end;
  font-family: Inter;
}
</style>
