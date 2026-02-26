<script setup lang="ts">
import { inject, ref, computed } from 'vue';
import { Search, Filter, ArrowRight, Zap, Clock, ShieldCheck } from 'lucide-vue-next';

const currentLang = inject<any>('lang');

const categories = computed(() => [
  { id: 'all', name: { zh: '全部', tc: '全部', en: 'All' } },
  { id: 'led', name: { zh: 'LED光管', tc: 'LED光管', en: 'LED Tubes' } },
  { id: 'energy', name: { zh: '节能光管', tc: '節能光管', en: 'Energy-Saving' } },
  { id: 'deco', name: { zh: '装饰光管', tc: '裝飾光管', en: 'Decorative' } }
]);

const activeCategory = ref('all');
const searchQuery = ref('');

const products = computed(() => [
  {
    id: 1,
    category: 'led',
    name: { zh: 'Pro-LED 工业级光管', tc: 'Pro-LED 工業級光管', en: 'Pro-LED Industrial Tube' },
    desc: { zh: '高亮度，适用于工厂和仓库。', tc: '高亮度，適用於工廠和倉庫。', en: 'High brightness, suitable for factories and warehouses.' },
    price: 'HK$ 120',
    specs: { zh: '20W, 2400lm, 50000h', tc: '20W, 2400lm, 50000h', en: '20W, 2400lm, 50000h' },
    img: 'public/images/led-06.jpg',
    alt: 'energy-saving LED tube in factory setting'
  },
  {
    id: 2,
    category: 'led',
    name: { zh: 'Office-Soft 办公柔光管', tc: 'Office-Soft 辦公柔光管', en: 'Office-Soft Tube' },
    desc: { zh: '防眩光设计，保护视力。', tc: '防眩光設計，保護視力。', en: 'Anti-glare design, eye protection.' },
    price: 'HK$ 85',
    specs: { zh: '15W, 1600lm, 40000h', tc: '15W, 1600lm, 40000h', en: '15W, 1600lm, 40000h' },
    img: 'public/images/led-07.png',
    alt: 'LED tube in office setting'
  },
  {
    id: 3,
    category: 'energy',
    name: { zh: 'Eco-Save 经典节能管', tc: 'Eco-Save 經典節能管', en: 'Eco-Save Classic' },
    desc: { zh: '高性价比，家庭首选。', tc: '高性價比，家庭首選。', en: 'Cost-effective, best for home.' },
    price: 'HK$ 45',
    specs: { zh: '18W, 1400lm, 20000h', tc: '18W, 1400lm, 20000h', en: '18W, 1400lm, 20000h' },
    img: 'public/images/led-08.png',
    alt: 'energy-saving light tube in home setting'
  },
  {
    id: 4,
    category: 'deco',
    name: { zh: 'Neon-Vibe 装饰霓虹管', tc: 'Neon-Vibe 裝飾霓虹管', en: 'Neon-Vibe Deco' },
    desc: { zh: '多种色彩，营造独特氛围。', tc: '多種色彩，營造獨特氛圍。', en: 'Multiple colors for unique atmosphere.' },
    price: 'HK$ 150',
    specs: { zh: '10W, RGB, 30000h', tc: '10W, RGB, 30000h', en: '10W, RGB, 30000h' },
    img: 'public/images/led-09.png',
    alt: 'decorative light tube in retail environment'
  },
  {
    id: 5,
    category: 'led',
    name: { zh: 'Slim-Line 嵌入式光管', tc: 'Slim-Line 嵌入式光管', en: 'Slim-Line Integrated' },
    desc: { zh: '超薄设计，节省空间。', tc: '超薄設計，節省空間。', en: 'Ultra-slim design, space saving.' },
    price: 'HK$ 95',
    specs: { zh: '12W, 1200lm, 45000h', tc: '12W, 1200lm, 45000h', en: '12W, 1200lm, 45000h' },
    img: 'public/images/led-10.jpg',
    alt: 'slim LED tube in modern kitchen'
  }
]);

const filteredProducts = computed(() => {
  return products.value.filter(p => {
    const matchesCategory = activeCategory.value === 'all' || p.category === activeCategory.value;
    const matchesSearch = p.name[currentLang.value].toLowerCase().includes(searchQuery.value.toLowerCase()) ||
                         p.desc[currentLang.value].toLowerCase().includes(searchQuery.value.toLowerCase());
    return matchesCategory && matchesSearch;
  });
});

const t = (obj: any) => obj[currentLang.value];
</script>

<template>
  <div class="py-16 bg-stone-50 min-h-screen">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <!-- Header -->
      <div class="mb-12">
        <h1 class="text-4xl font-bold text-stone-900 mb-4">
          {{ currentLang === 'en' ? 'Our Products' : (currentLang === 'zh' ? '我们的产品' : '我們的產品') }}
        </h1>
        <p class="text-stone-600 max-w-2xl">
          {{ currentLang === 'en' ? 'Discover our range of high-performance light tubes designed for every need.' : (currentLang === 'zh' ? '探索我们为各种需求设计的高性能光管系列。' : '探索我們為各種需求設計的高性能光管系列。') }}
        </p>
      </div>

      <!-- Filters & Search -->
      <div class="flex flex-col md:flex-row justify-between items-start md:items-center gap-6 mb-12">
        <div class="flex flex-wrap gap-2">
          <button 
            v-for="cat in categories" 
            :key="cat.id"
            @click="activeCategory = cat.id"
            :class="[
              'px-6 py-2.5 rounded-full text-sm font-medium transition-all',
              activeCategory === cat.id 
                ? 'bg-emerald-600 text-white shadow-lg shadow-emerald-200' 
                : 'bg-white text-stone-600 hover:bg-stone-100 border border-stone-200'
            ]"
          >
            {{ t(cat.name) }}
          </button>
        </div>

        <div class="relative w-full md:w-80">
          <Search class="absolute left-4 top-1/2 -translate-y-1/2 w-4 h-4 text-stone-400" />
          <input 
            v-model="searchQuery"
            type="text" 
            :placeholder="currentLang === 'en' ? 'Search products...' : (currentLang === 'zh' ? '搜索产品...' : '搜索產品...')"
            class="w-full pl-11 pr-4 py-2.5 bg-white border border-stone-200 rounded-full text-sm focus:outline-none focus:ring-2 focus:ring-emerald-500/20 focus:border-emerald-500 transition-all"
          />
        </div>
      </div>

      <!-- Product Grid -->
      <div v-if="filteredProducts.length > 0" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-8">
        <div 
          v-for="product in filteredProducts" 
          :key="product.id"
          class="bg-white rounded-3xl border border-stone-200 overflow-hidden hover:shadow-2xl transition-all duration-500 group"
        >
          <div class="aspect-[4/3] overflow-hidden relative">
            <img 
              :src="product.img" 
              :alt="product.alt"
              class="w-full h-full object-cover transition-transform duration-700 group-hover:scale-110"
              referrerpolicy="no-referrer"
            />
            <div class="absolute top-4 left-4">
              <span class="px-3 py-1 bg-white/90 backdrop-blur-md rounded-full text-[10px] font-bold uppercase tracking-widest text-emerald-600 border border-emerald-100">
                {{ t(categories.find(c => c.id === product.category)?.name) }}
              </span>
            </div>
          </div>
          
          <div class="p-8">
            <div class="flex justify-between items-start mb-4">
              <h3 class="text-xl font-bold text-stone-900">{{ t(product.name) }}</h3>
              <span class="text-emerald-600 font-bold">{{ product.price }}</span>
            </div>
            <p class="text-stone-600 text-sm mb-6 leading-relaxed">
              {{ t(product.desc) }}
            </p>
            
            <div class="grid grid-cols-3 gap-4 mb-8">
              <div class="flex flex-col items-center text-center">
                <Zap class="w-4 h-4 text-stone-400 mb-2" />
                <span class="text-[10px] text-stone-500 uppercase tracking-tighter">{{ product.specs[currentLang].split(',')[0] }}</span>
              </div>
              <div class="flex flex-col items-center text-center border-x border-stone-100">
                <Clock class="w-4 h-4 text-stone-400 mb-2" />
                <span class="text-[10px] text-stone-500 uppercase tracking-tighter">{{ product.specs[currentLang].split(',')[2] }}</span>
              </div>
              <div class="flex flex-col items-center text-center">
                <ShieldCheck class="w-4 h-4 text-stone-400 mb-2" />
                <span class="text-[10px] text-stone-500 uppercase tracking-tighter">Warranty</span>
              </div>
            </div>

            <button class="w-full py-3 bg-stone-900 text-white rounded-xl font-semibold hover:bg-emerald-600 transition-colors flex items-center justify-center group">
              {{ currentLang === 'en' ? 'View Details' : (currentLang === 'zh' ? '查看详情' : '查看詳情') }}
              <ArrowRight class="ml-2 w-4 h-4 group-hover:translate-x-1 transition-transform" />
            </button>
          </div>
        </div>
      </div>

      <!-- Empty State -->
      <div v-else class="py-24 text-center">
        <div class="w-20 h-20 bg-stone-100 rounded-full flex items-center justify-center mx-auto mb-6">
          <Search class="w-8 h-8 text-stone-300" />
        </div>
        <h3 class="text-xl font-bold text-stone-900 mb-2">
          {{ currentLang === 'en' ? 'No products found' : (currentLang === 'zh' ? '未找到产品' : '未找到產品') }}
        </h3>
        <p class="text-stone-500">
          {{ currentLang === 'en' ? 'Try adjusting your search or filter to find what you are looking for.' : (currentLang === 'zh' ? '尝试调整您的搜索或过滤器以找到您想要的内容。' : '嘗試調整您的搜索或過濾器以找到您想要的內容。') }}
        </p>
        <button @click="activeCategory = 'all'; searchQuery = ''" class="mt-8 text-emerald-600 font-semibold hover:underline">
          {{ currentLang === 'en' ? 'Clear all filters' : (currentLang === 'zh' ? '清除所有过滤器' : '清除所有過濾器') }}
        </button>
      </div>
    </div>
  </div>
</template>
