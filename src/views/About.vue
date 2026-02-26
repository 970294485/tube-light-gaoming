<script setup lang="ts">
import { inject, computed } from 'vue';
import { Target, Eye, Award, Globe2, Users2, Recycle } from 'lucide-vue-next';

const currentLang = inject<any>('lang');

const content = computed(() => ({
  title: { zh: '关于高明照明', tc: '關於高明照明', en: 'About Gao Ming Lighting' },
  mission: {
    title: { zh: '我们的使命', tc: '我們的使命', en: 'Our Mission' },
    text: { 
      zh: '高明照明致力于通过创新的LED技术，为全球客户提供高效、环保、耐用的照明解决方案。我们相信，光不仅是照明，更是提升生活品质和工作效率的关键。', 
      tc: '高明照明致力於通過創新的LED技術，為全球客戶提供高效、環保、耐用的照明解決方案。我們相信，光不僅是照明，更是提升生活品質和工作效率的關鍵。', 
      en: 'Gao Ming Lighting is dedicated to providing efficient, eco-friendly, and durable lighting solutions through innovative LED technology. We believe light is not just illumination, but a key to enhancing quality of life and work efficiency.' 
    }
  },
  values: [
    {
      icon: Target,
      title: { zh: '创新驱动', tc: '創新驅動', en: 'Innovation' },
      desc: { zh: '不断研发新技术，引领行业标准。', tc: '不斷研發新技術，引領行業標準。', en: 'Constantly developing new technologies to lead industry standards.' }
    },
    {
      icon: Recycle,
      title: { zh: '可持续发展', tc: '可持續發展', en: 'Sustainability' },
      desc: { zh: '承诺减少碳足迹，推广绿色能源。', tc: '承諾減少碳足跡，推廣綠色能源。', en: 'Committed to reducing carbon footprint and promoting green energy.' }
    },
    {
      icon: Award,
      title: { zh: '卓越品质', tc: '卓越品質', en: 'Quality Excellence' },
      desc: { zh: '严格的质量控制，确保每一支光管都完美无瑕。', tc: '嚴格的質量控制，確保每一支光管都完美無瑕。', en: 'Strict quality control ensuring every tube is flawless.' }
    }
  ],
  stats: [
    { label: { zh: '成立年份', tc: '成立年份', en: 'Founded' }, value: '2008' },
    { label: { zh: '出口国家', tc: '出口國家', en: 'Countries' }, value: '35+' },
    { label: { zh: '专利技术', tc: '專利技術', en: 'Patents' }, value: '120+' },
    { label: { zh: '满意客户', tc: '滿意客戶', en: 'Happy Clients' }, value: '10k+' }
  ]
}));

const t = (obj: any) => obj[currentLang.value];
</script>

<template>
  <div class="bg-white">
    <!-- Hero -->
    <section class="relative py-24 bg-stone-900 overflow-hidden">
      <div class="absolute inset-0 opacity-20">
        <img src="/public/images/led-12.jpg" class="w-full h-full object-cover" referrerpolicy="no-referrer" />
      </div>
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 relative z-10 text-center">
        <h1 class="text-4xl md:text-6xl font-bold text-white mb-6 tracking-tight">{{ t(content.title) }}</h1>
        <p class="text-stone-400 text-lg max-w-2xl mx-auto leading-relaxed">
          {{ currentLang === 'en' ? 'A decade of excellence in lighting technology, serving industries and homes worldwide.' : (currentLang === 'zh' ? '十余年照明技术卓越历程，服务全球工业与家庭。' : '十餘年照明技術卓越歷程，服務全球工業與家庭。') }}
        </p>
      </div>
    </section>

    <!-- Mission -->
    <section class="py-24">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="grid grid-cols-1 lg:grid-cols-2 gap-16 items-center">
          <div class="relative">
            <div class="aspect-square rounded-3xl overflow-hidden shadow-2xl">
              <img src="/public/images/led-13.jpg" class="w-full h-full object-cover" alt="Gao Ming Mission" referrerpolicy="no-referrer" />
            </div>
            <div class="absolute -bottom-8 -right-8 bg-emerald-600 p-8 rounded-3xl shadow-xl hidden md:block">
              <Globe2 class="text-white w-12 h-12" />
            </div>
          </div>
          
          <div>
            <span class="text-emerald-600 font-bold uppercase tracking-widest text-sm mb-4 block">{{ t(content.mission.title) }}</span>
            <h2 class="text-3xl md:text-4xl font-bold text-stone-900 mb-8 leading-tight">{{ t(content.mission.title) }}</h2>
            <p class="text-stone-600 text-lg leading-relaxed mb-10">
              {{ t(content.mission.text) }}
            </p>
            
            <div class="grid grid-cols-2 gap-8">
              <div v-for="stat in content.stats" :key="stat.label.en">
                <div class="text-3xl font-bold text-stone-900 mb-1">{{ stat.value }}</div>
                <div class="text-sm text-stone-500 uppercase tracking-wider">{{ t(stat.label) }}</div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Values -->
    <section class="py-24 bg-stone-50">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="text-center mb-16">
          <h2 class="text-3xl font-bold text-stone-900">{{ currentLang === 'en' ? 'Our Core Values' : (currentLang === 'zh' ? '我们的核心价值' : '我們的核心價值') }}</h2>
        </div>
        
        <div class="grid grid-cols-1 md:grid-cols-3 gap-12">
          <div v-for="value in content.values" :key="value.title.en" class="text-center">
            <div class="w-20 h-20 bg-white rounded-full flex items-center justify-center mx-auto mb-8 shadow-lg">
              <component :is="value.icon" class="text-emerald-600 w-8 h-8" />
            </div>
            <h3 class="text-xl font-bold text-stone-900 mb-4">{{ t(value.title) }}</h3>
            <p class="text-stone-600 leading-relaxed">{{ t(value.desc) }}</p>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>
