<script setup lang="ts">
import { ref, provide, computed } from 'vue';
import { useRouter } from 'vue-router';
import { Globe, Menu, X, Lightbulb, Mail, Phone, MapPin, Facebook, Instagram, Twitter } from 'lucide-vue-next';

// Language state
const currentLang = ref<'zh' | 'tc' | 'en'>('zh');
const languages = [
  { code: 'zh', name: '简体中文' },
  { code: 'tc', name: '繁體中文' },
  { code: 'en', name: 'English' }
];

const setLanguage = (lang: 'zh' | 'tc' | 'en') => {
  currentLang.value = lang;
};

provide('lang', currentLang);
provide('setLang', setLanguage);

// Navigation
const isMenuOpen = ref(false);
const router = useRouter();

const navItems = computed(() => [
  { name: { zh: '首页', tc: '首頁', en: 'Home' }, path: '/' },
  { name: { zh: '产品', tc: '產品', en: 'Products' }, path: '/products' },
  { name: { zh: '关于我们', tc: '關於我們', en: 'About' }, path: '/about' },
  { name: { zh: '联系我们', tc: '聯繫我們', en: 'Contact' }, path: '/contact' }
]);

const t = (key: string) => {
  const translations: any = {
    companyName: { zh: '高明照明', tc: '高明照明', en: 'Gao Ming Lighting' },
    footerDesc: { 
      zh: '致力于提供高质量、节能的照明解决方案。', 
      tc: '致力于提供高品質、節能的照明解決方案。', 
      en: 'Dedicated to providing high-quality, energy-efficient lighting solutions.' 
    },
    rights: { zh: '版权所有', tc: '版權所有', en: 'All Rights Reserved' }
  };
  return translations[key]?.[currentLang.value] || key;
};
</script>

<template>
  <div class="min-h-screen bg-stone-50 font-sans text-stone-900">
    <!-- Header -->
    <header class="sticky top-0 z-50 bg-white/80 backdrop-blur-md border-b border-stone-200">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="flex justify-between items-center h-20">
          <!-- Logo -->
          <router-link to="/" class="flex items-center space-x-2">
            <div class="w-10 h-10 bg-emerald-600 rounded-lg flex items-center justify-center">
              <Lightbulb class="text-white w-6 h-6" />
            </div>
            <span class="text-2xl font-bold tracking-tight text-stone-900">{{ t('companyName') }}</span>
          </router-link>

          <!-- Desktop Nav -->
          <nav class="hidden md:flex items-center space-x-8">
            <router-link 
              v-for="item in navItems" 
              :key="item.path" 
              :to="item.path"
              class="text-sm font-medium text-stone-600 hover:text-emerald-600 transition-colors"
              active-class="text-emerald-600"
            >
              {{ item.name[currentLang] }}
            </router-link>
            
            <!-- Lang Switcher -->
            <div class="relative group">
              <button class="flex items-center space-x-1 text-sm font-medium text-stone-600 hover:text-emerald-600">
                <Globe class="w-4 h-4" />
                <span>{{ languages.find(l => l.code === currentLang)?.name }}</span>
              </button>
              <div class="absolute right-0 mt-2 w-40 bg-white border border-stone-200 rounded-xl shadow-lg opacity-0 invisible group-hover:opacity-100 group-hover:visible transition-all duration-200 py-2">
                <button 
                  v-for="lang in languages" 
                  :key="lang.code"
                  @click="setLanguage(lang.code as any)"
                  class="w-full text-left px-4 py-2 text-sm text-stone-600 hover:bg-stone-50 hover:text-emerald-600"
                >
                  {{ lang.name }}
                </button>
              </div>
            </div>
          </nav>

          <!-- Mobile Menu Button -->
          <div class="md:hidden flex items-center space-x-4">
             <!-- Mobile Lang Switcher -->
             <button @click="setLanguage(currentLang === 'en' ? 'zh' : currentLang === 'zh' ? 'tc' : 'en')" class="text-stone-600">
                <Globe class="w-5 h-5" />
             </button>
            <button @click="isMenuOpen = !isMenuOpen" class="text-stone-600">
              <component :is="isMenuOpen ? X : Menu" class="w-6 h-6" />
            </button>
          </div>
        </div>
      </div>

      <!-- Mobile Nav -->
      <div v-if="isMenuOpen" class="md:hidden bg-white border-b border-stone-200 py-4 px-4 space-y-4">
        <router-link 
          v-for="item in navItems" 
          :key="item.path" 
          :to="item.path"
          @click="isMenuOpen = false"
          class="block text-base font-medium text-stone-600 hover:text-emerald-600"
          active-class="text-emerald-600"
        >
          {{ item.name[currentLang] }}
        </router-link>
      </div>
    </header>

    <!-- Main Content -->
    <main>
      <router-view v-slot="{ Component }">
        <transition name="fade" mode="out-in">
          <component :is="Component" />
        </transition>
      </router-view>
    </main>

    <!-- Footer -->
    <footer class="bg-stone-900 text-stone-400 py-16">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="grid grid-cols-1 md:grid-cols-4 gap-12">
          <div class="col-span-1 md:col-span-2">
            <div class="flex items-center space-x-2 mb-6">
              <div class="w-8 h-8 bg-emerald-600 rounded flex items-center justify-center">
                <Lightbulb class="text-white w-5 h-5" />
              </div>
              <span class="text-xl font-bold text-white">{{ t('companyName') }}</span>
            </div>
            <p class="max-w-md text-sm leading-relaxed">
              {{ t('footerDesc') }}
            </p>
          </div>
          
          <div>
            <h4 class="text-white font-semibold mb-6 uppercase tracking-wider text-xs">{{ currentLang === 'en' ? 'Quick Links' : (currentLang === 'zh' ? '快速链接' : '快速鏈接') }}</h4>
            <ul class="space-y-4 text-sm">
              <li v-for="item in navItems" :key="item.path">
                <router-link :to="item.path" class="hover:text-emerald-400 transition-colors">
                  {{ item.name[currentLang] }}
                </router-link>
              </li>
            </ul>
          </div>

          <div>
            <h4 class="text-white font-semibold mb-6 uppercase tracking-wider text-xs">{{ currentLang === 'en' ? 'Contact' : (currentLang === 'zh' ? '联系方式' : '聯繫方式') }}</h4>
            <ul class="space-y-4 text-sm">
              <li class="flex items-start space-x-3">
                <MapPin class="w-4 h-4 mt-0.5 shrink-0" />
                <span>{{ currentLang === 'en' ? '123 Lighting Ave, Industrial District, HK' : (currentLang === 'zh' ? '香港工业区照明大道123号' : '香港工業區照明大道123號') }}</span>
              </li>
              <li class="flex items-center space-x-3">
                <Phone class="w-4 h-4 shrink-0" />
                <span>+852 2345 6789</span>
              </li>
              <li class="flex items-center space-x-3">
                <Mail class="w-4 h-4 shrink-0" />
                <span>info@gaominglighting.com</span>
              </li>
            </ul>
          </div>
        </div>
        
        <div class="mt-16 pt-8 border-t border-stone-800 flex flex-col md:flex-row justify-between items-center space-y-4 md:space-y-0 text-xs">
          <p>&copy; 2024 {{ t('companyName') }}. {{ t('rights') }}.</p>
          <div class="flex space-x-6">
            <Facebook class="w-4 h-4 hover:text-white cursor-pointer" />
            <Instagram class="w-4 h-4 hover:text-white cursor-pointer" />
            <Twitter class="w-4 h-4 hover:text-white cursor-pointer" />
          </div>
        </div>
      </div>
    </footer>
  </div>
</template>

<style>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

@import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap');

body {
  font-family: 'Inter', sans-serif;
}
</style>
