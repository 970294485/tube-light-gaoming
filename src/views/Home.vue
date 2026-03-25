<script setup lang="ts">
import { inject, computed } from 'vue';
import { ArrowRight, Zap, Shield, Leaf, Building2, Store, Factory, Home as HomeIcon } from 'lucide-vue-next';

const currentLang = inject<any>('lang');

const content = computed(() => ({
  heroTitle: {
    zh: '点亮您的未来，高明照明',
    tc: '點亮您的未來，高明照明',
    en: 'Light Up Your Future with Gao Ming'
  },
  heroSub: {
    zh: '专业LED与节能光管解决方案，为您的空间带来高效、耐用、环保的光芒。',
    tc: '專業LED與節能光管解決方案，為您的空間帶來高效、耐用、環保的光芒。',
    en: 'Professional LED and energy-saving tube solutions, bringing efficient, durable, and eco-friendly light to your space.'
  },
  cta: {
    zh: '探索产品',
    tc: '探索產品',
    en: 'Explore Products'
  },
  // 业务范围
  businessScopeTitle: {
    zh: '我们的业务范围',
    tc: '我們的業務範圍',
    en: 'Our Business Scope'
  },
  businessScopes: [
    {
      icon: Building2,
      title: { zh: '商业照明', tc: '商業照明', en: 'Commercial Lighting' },
      desc: { zh: '为办公室、商场和酒店提供专业照明设计。', tc: '為辦公室、商場和酒店提供專業照明設計。', en: 'Professional lighting design for offices, malls, and hotels.' }
    },
    {
      icon: Factory,
      title: { zh: '工业照明', tc: '工業照明', en: 'Industrial Lighting' },
      desc: { zh: '高亮度、耐用型方案，适用于工厂和仓库。', tc: '高亮度、耐用型方案，適用於工廠和倉庫。', en: 'High-brightness, durable solutions for factories and warehouses.' }
    },
    {
      icon: HomeIcon,
      title: { zh: '家居照明', tc: '家居照明', en: 'Residential Lighting' },
      desc: { zh: '营造温馨舒适的家庭光影环境。', tc: '營造溫馨舒適的家庭光影環境。', en: 'Creating warm and comfortable lighting environments for homes.' }
    }
  ],
  // 产品介绍
  productIntroTitle: {
    zh: '产品介绍',
    tc: '產品介紹',
    en: 'Product Introduction'
  },
  productIntros: [
    {
      name: { zh: 'LED光管系列', tc: 'LED光管系列', en: 'LED Tube Series' },
      desc: { zh: '采用最新芯片技术，超高光效。', tc: '採用最新芯片技術，超高光效。', en: 'Using the latest chip technology for ultra-high efficiency.' },
      img: '/images/led-01.webp'
      
    },
    {
      name: { zh: '节能光管系列', tc: '節能光管系列', en: 'Energy-Saving Series' },
      desc: { zh: '经典稳定，极致节能。', tc: '經典穩定，極致節能。', en: 'Classic stability with extreme energy savings.' },
      img: '/images/led-02.png'
    },
    {
      name: { zh: '装饰光管系列', tc: '裝飾光管系列', en: 'Decorative Series' },
      desc: { zh: '色彩丰富，满足个性化装饰需求。', tc: '色彩豐富，滿足個性化裝飾需求。', en: 'Rich colors to meet personalized decorative needs.' },
      img: '/images/led-03.webp'
    }
  ],
  // 案例分享
  caseSharingTitle: {
    zh: '案例分享',
    tc: '案例分享',
    en: 'Case Sharing'
  },
  cases: [
    {
      title: { zh: '中环国际金融中心办公区', tc: '中環國際金融中心辦公區', en: 'IFC Office Area' },
      img: '/images/led-04.webp',
      tag: { zh: '商业', tc: '商業', en: 'Commercial' }
    },
    {
      title: { zh: '九龙湾旗舰零售店', tc: '九龍灣旗艦零售店', en: 'Kowloon Bay Flagship Store' },
      img: 'https://images.unsplash.com/photo-1567401893414-76b7b1e5a7a5?auto=format&fit=crop&w=800&q=80',
      tag: { zh: '零售', tc: '零售', en: 'Retail' }
    },
    {
      title: { zh: '新界自动化物流仓库', tc: '新界自動化物流倉庫', en: 'NT Automated Warehouse' },
      img: '/images/led-05.png',
      tag: { zh: '工业', tc: '工業', en: 'Industrial' }
    }
  ],
  // 产品亮点
  highlightsTitle: {
    zh: '产品亮点',
    tc: '產品亮點',
    en: 'Product Highlights'
  },
  highlights: [
    {
      icon: Zap,
      title: { zh: '极致节能', tc: '極致節能', en: 'Extreme Efficiency' },
      desc: { zh: '比传统光源节能80%以上。', tc: '比傳統光源節能80%以上。', en: 'Over 80% energy savings compared to traditional sources.' }
    },
    {
      icon: Shield,
      title: { zh: '超长寿命', tc: '超長壽命', en: 'Ultra Long Life' },
      desc: { zh: '50,000小时使用寿命，减少更换频率。', tc: '50,000小時使用壽命，減少更換頻率。', en: '50,000 hours lifespan, reducing replacement frequency.' }
    },
    {
      icon: Leaf,
      title: { zh: '绿色环保', tc: '綠色環保', en: 'Eco-Friendly' },
      desc: { zh: '无汞、无紫外线，符合RoHS标准。', tc: '無汞、無紫外線，符合RoHS標準。', en: 'Mercury-free, UV-free, RoHS compliant.' }
    }
  ]
}));

const t = (obj: any) => obj[currentLang.value];
</script>

<template>
  <div class="overflow-hidden">
    <!-- Hero Section -->
    <section class="relative h-[90vh] flex items-center">
      <div class="absolute inset-0 z-0">
        <img 
          src="https://images.unsplash.com/photo-1497366216548-37526070297c?auto=format&fit=crop&w=1920&q=80" 
          class="w-full h-full object-cover brightness-50"
          alt="Modern lighting background"
          referrerpolicy="no-referrer"
        />
      </div>
      
      <div class="relative z-10 max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 text-white">
        <div class="max-w-3xl">
          <h1 class="text-5xl md:text-7xl font-bold leading-tight mb-6 tracking-tight">
            {{ t(content.heroTitle) }}
          </h1>
          <p class="text-xl md:text-2xl text-stone-200 mb-10 leading-relaxed font-light">
            {{ t(content.heroSub) }}
          </p>
          <div class="flex flex-col sm:flex-row space-y-4 sm:space-y-0 sm:space-x-6">
            <router-link to="/products" class="inline-flex items-center justify-center px-8 py-4 bg-emerald-600 hover:bg-emerald-500 text-white rounded-full font-semibold transition-all group">
              {{ t(content.cta) }}
              <ArrowRight class="ml-2 w-5 h-5 group-hover:translate-x-1 transition-transform" />
            </router-link>
            <router-link to="/about" class="inline-flex items-center justify-center px-8 py-4 bg-white/10 hover:bg-white/20 backdrop-blur-md text-white border border-white/30 rounded-full font-semibold transition-all">
              {{ currentLang === 'en' ? 'Learn More' : (currentLang === 'zh' ? '了解更多' : '了解更多') }}
            </router-link>
          </div>
        </div>
      </div>
    </section>

    <!-- Business Scope Section -->
    <section class="py-24 bg-white">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="text-center mb-20">
          <h2 class="text-3xl md:text-4xl font-bold text-stone-900 mb-4">{{ t(content.businessScopeTitle) }}</h2>
          <div class="w-20 h-1.5 bg-emerald-600 mx-auto rounded-full"></div>
        </div>
        
        <div class="grid grid-cols-1 md:grid-cols-3 gap-12">
          <div v-for="scope in content.businessScopes" :key="scope.title.en" class="p-8 rounded-3xl bg-stone-50 border border-stone-100 hover:shadow-xl transition-all duration-300 text-center">
            <div class="w-16 h-16 bg-emerald-100 rounded-2xl flex items-center justify-center mb-6 mx-auto">
              <component :is="scope.icon" class="text-emerald-600 w-8 h-8" />
            </div>
            <h3 class="text-xl font-bold text-stone-900 mb-4">{{ t(scope.title) }}</h3>
            <p class="text-stone-600 leading-relaxed">{{ t(scope.desc) }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Product Introduction Section -->
    <section class="py-24 bg-stone-50">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="text-center mb-20">
          <h2 class="text-3xl md:text-4xl font-bold text-stone-900 mb-4">{{ t(content.productIntroTitle) }}</h2>
          <div class="w-20 h-1.5 bg-emerald-600 mx-auto rounded-full"></div>
        </div>
        
        <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
          <div v-for="intro in content.productIntros" :key="intro.name.en" class="bg-white rounded-3xl overflow-hidden border border-stone-200 group">
            <div class="aspect-video overflow-hidden">
              <img :src="intro.img" class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-500" referrerpolicy="no-referrer" />
            </div>
            <div class="p-8">
              <h3 class="text-xl font-bold text-stone-900 mb-2">{{ t(intro.name) }}</h3>
              <p class="text-stone-600 mb-6">{{ t(intro.desc) }}</p>
              <router-link to="/products" class="text-emerald-600 font-semibold flex items-center hover:underline">
                {{ currentLang === 'en' ? 'View Products' : (currentLang === 'zh' ? '查看产品' : '查看產品') }}
                <ArrowRight class="ml-2 w-4 h-4" />
              </router-link>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Case Sharing Section -->
    <section class="py-24 bg-white">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="flex flex-col md:flex-row justify-between items-end mb-16 space-y-6 md:space-y-0">
          <div class="max-w-2xl">
            <h2 class="text-3xl md:text-4xl font-bold text-stone-900 mb-4">{{ t(content.caseSharingTitle) }}</h2>
            <p class="text-stone-600">{{ currentLang === 'en' ? 'Explore how our lighting solutions transform various spaces.' : (currentLang === 'zh' ? '探索我们的照明解决方案如何改变各种空间。' : '探索我們的照明解決方案如何改變各種空間。') }}</p>
          </div>
          <router-link to="/about" class="text-emerald-600 font-semibold flex items-center hover:underline">
            {{ currentLang === 'en' ? 'More Cases' : (currentLang === 'zh' ? '更多案例' : '更多案例') }}
            <ArrowRight class="ml-2 w-4 h-4" />
          </router-link>
        </div>

        <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-8">
          <div v-for="item in content.cases" :key="item.title.en" class="group relative overflow-hidden rounded-3xl aspect-[4/3]">
            <img 
              :src="item.img" 
              class="w-full h-full object-cover transition-transform duration-700 group-hover:scale-110"
              referrerpolicy="no-referrer"
            />
            <div class="absolute inset-0 bg-gradient-to-t from-black/80 via-black/20 to-transparent flex flex-col justify-end p-8">
              <span class="text-emerald-400 text-xs font-bold uppercase tracking-widest mb-2">{{ t(item.tag) }}</span>
              <h3 class="text-xl font-bold text-white">{{ t(item.title) }}</h3>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Product Highlights Section -->
    <section class="py-24 bg-stone-900 text-white">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="text-center mb-20">
          <h2 class="text-3xl md:text-4xl font-bold mb-4">{{ t(content.highlightsTitle) }}</h2>
          <div class="w-20 h-1.5 bg-emerald-600 mx-auto rounded-full"></div>
        </div>
        
        <div class="grid grid-cols-1 md:grid-cols-3 gap-12">
          <div v-for="highlight in content.highlights" :key="highlight.title.en" class="text-center">
            <div class="w-20 h-20 bg-emerald-600/20 rounded-full flex items-center justify-center mx-auto mb-8">
              <component :is="highlight.icon" class="text-emerald-500 w-10 h-10" />
            </div>
            <h3 class="text-2xl font-bold mb-4">{{ t(highlight.title) }}</h3>
            <p class="text-stone-400 leading-relaxed">{{ t(highlight.desc) }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Newsletter/CTA -->
    <section class="py-24 bg-emerald-600 relative overflow-hidden">
      <div class="absolute top-0 right-0 -translate-y-1/2 translate-x-1/4 w-96 h-96 bg-emerald-500 rounded-full blur-3xl opacity-50"></div>
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 relative z-10 text-center">
        <h2 class="text-3xl md:text-5xl font-bold text-white mb-8">
          {{ currentLang === 'en' ? 'Ready to upgrade your lighting?' : (currentLang === 'zh' ? '准备好升级您的照明了吗？' : '準備好升級您的照明了嗎？') }}
        </h2>
        <p class="text-emerald-100 text-lg mb-12 max-w-2xl mx-auto">
          {{ currentLang === 'en' ? 'Contact our experts today for a free consultation and energy-saving audit.' : (currentLang === 'zh' ? '立即联系我们的专家，获取免费咨询和节能审计。' : '立即聯繫我們的專家，獲取免費諮詢和節能審計。') }}
        </p>
        <router-link to="/contact" class="inline-flex items-center justify-center px-10 py-4 bg-white text-emerald-600 rounded-full font-bold text-lg hover:bg-stone-100 transition-all">
          {{ currentLang === 'en' ? 'Get in Touch' : (currentLang === 'zh' ? '立即联系' : '立即聯繫') }}
        </router-link>
      </div>
    </section>
  </div>
</template>
