<script setup lang="ts">
import { inject, ref, reactive } from 'vue';
import { Send, Phone, Mail, MapPin, Clock, CheckCircle2 } from 'lucide-vue-next';

const currentLang = inject<any>('lang');

const form = reactive({
  name: '',
  email: '',
  subject: '',
  message: ''
});

const errors = reactive({
  name: '',
  email: '',
  message: ''
});

const isSubmitted = ref(false);
const isSubmitting = ref(false);

const validate = () => {
  let isValid = true;
  errors.name = '';
  errors.email = '';
  errors.message = '';

  if (!form.name) {
    errors.name = currentLang.value === 'en' ? 'Name is required' : (currentLang.value === 'zh' ? '请输入姓名' : '請輸入姓名');
    isValid = false;
  }
  if (!form.email || !/^\S+@\S+\.\S+$/.test(form.email)) {
    errors.email = currentLang.value === 'en' ? 'Valid email is required' : (currentLang.value === 'zh' ? '请输入有效的电子邮箱' : '請輸入有效的電子郵箱');
    isValid = false;
  }
  if (!form.message) {
    errors.message = currentLang.value === 'en' ? 'Message is required' : (currentLang.value === 'zh' ? '请输入留言内容' : '請輸入留言內容');
    isValid = false;
  }

  return isValid;
};

const handleSubmit = async () => {
  if (!validate()) return;

  isSubmitting.value = true;
  // Simulate API call
  await new Promise(resolve => setTimeout(resolve, 1500));
  
  isSubmitting.value = false;
  isSubmitted.value = true;
  
  // Reset form
  form.name = '';
  form.email = '';
  form.subject = '';
  form.message = '';

  setTimeout(() => {
    isSubmitted.value = false;
  }, 5000);
};
</script>

<template>
  <div class="py-24 bg-stone-50">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="grid grid-cols-1 lg:grid-cols-2 gap-20">
        <!-- Info -->
        <div>
          <h1 class="text-4xl font-bold text-stone-900 mb-8">
            {{ currentLang === 'en' ? 'Get in Touch' : (currentLang === 'zh' ? '联系我们' : '聯繫我們') }}
          </h1>
          <p class="text-stone-600 text-lg mb-12 leading-relaxed">
            {{ currentLang === 'en' ? 'Have questions about our products or need a custom lighting solution? Our team is here to help.' : (currentLang === 'zh' ? '对我们的产品有疑问或需要定制照明解决方案？我们的团队随时为您提供帮助。' : '對我們的產品有疑問或需要定制照明解決方案？我們的團隊隨時為您提供幫助。') }}
          </p>

          <div class="space-y-8">
            <div class="flex items-start space-x-6">
              <div class="w-12 h-12 bg-white rounded-2xl flex items-center justify-center shadow-sm border border-stone-100 shrink-0">
                <MapPin class="text-emerald-600 w-6 h-6" />
              </div>
              <div>
                <h4 class="font-bold text-stone-900 mb-1">{{ currentLang === 'en' ? 'Our Location' : (currentLang === 'zh' ? '公司地址' : '公司地址') }}</h4>
                <p class="text-stone-500 text-sm">{{ currentLang === 'en' ? '123 Lighting Ave, Industrial District, Hong Kong' : (currentLang === 'zh' ? '香港工业区照明大道123号' : '香港工業區照明大道123號') }}</p>
              </div>
            </div>

            <div class="flex items-start space-x-6">
              <div class="w-12 h-12 bg-white rounded-2xl flex items-center justify-center shadow-sm border border-stone-100 shrink-0">
                <Phone class="text-emerald-600 w-6 h-6" />
              </div>
              <div>
                <h4 class="font-bold text-stone-900 mb-1">{{ currentLang === 'en' ? 'Phone' : (currentLang === 'zh' ? '联系电话' : '聯繫電話') }}</h4>
                <p class="text-stone-500 text-sm">+852 2345 6789</p>
              </div>
            </div>

            <div class="flex items-start space-x-6">
              <div class="w-12 h-12 bg-white rounded-2xl flex items-center justify-center shadow-sm border border-stone-100 shrink-0">
                <Mail class="text-emerald-600 w-6 h-6" />
              </div>
              <div>
                <h4 class="font-bold text-stone-900 mb-1">{{ currentLang === 'en' ? 'Email' : (currentLang === 'zh' ? '电子邮箱' : '電子郵箱') }}</h4>
                <p class="text-stone-500 text-sm">info@gaominglighting.com</p>
              </div>
            </div>

            <div class="flex items-start space-x-6">
              <div class="w-12 h-12 bg-white rounded-2xl flex items-center justify-center shadow-sm border border-stone-100 shrink-0">
                <Clock class="text-emerald-600 w-6 h-6" />
              </div>
              <div>
                <h4 class="font-bold text-stone-900 mb-1">{{ currentLang === 'en' ? 'Working Hours' : (currentLang === 'zh' ? '营业时间' : '營業時間') }}</h4>
                <p class="text-stone-500 text-sm">{{ currentLang === 'en' ? 'Mon - Fri: 9:00 AM - 6:00 PM' : (currentLang === 'zh' ? '周一至周五：上午9:00 - 下午6:00' : '週一至週五：上午9:00 - 下午6:00') }}</p>
              </div>
            </div>
          </div>

          <!-- Simple Map Placeholder -->
          <div class="mt-12 rounded-3xl overflow-hidden h-64 bg-stone-200 relative border border-stone-300">
            <div class="absolute inset-0 flex items-center justify-center text-stone-400 font-medium">
               {{ currentLang === 'en' ? 'Map View' : (currentLang === 'zh' ? '地图视图' : '地圖視圖') }}
            </div>
            <img src="/public/images/led-14.jpg" class="w-full h-full object-cover opacity-50 grayscale" referrerpolicy="no-referrer" />
          </div>
        </div>

        <!-- Form -->
        <div class="bg-white rounded-[2.5rem] p-8 md:p-12 shadow-xl shadow-stone-200/50 border border-stone-100">
          <form @submit.prevent="handleSubmit" class="space-y-6">
            <div v-if="isSubmitted" class="p-4 bg-emerald-50 border border-emerald-100 rounded-2xl flex items-center space-x-3 text-emerald-700 animate-in fade-in slide-in-from-top-4">
              <CheckCircle2 class="w-5 h-5" />
              <span class="text-sm font-medium">{{ currentLang === 'en' ? 'Message sent successfully!' : (currentLang === 'zh' ? '留言发送成功！' : '留言發送成功！') }}</span>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
              <div class="space-y-2">
                <label class="text-xs font-bold text-stone-400 uppercase tracking-widest">{{ currentLang === 'en' ? 'Full Name' : (currentLang === 'zh' ? '姓名' : '姓名') }}</label>
                <input 
                  v-model="form.name"
                  type="text" 
                  class="w-full px-5 py-4 bg-stone-50 border border-stone-200 rounded-2xl focus:outline-none focus:ring-2 focus:ring-emerald-500/20 focus:border-emerald-500 transition-all"
                  :class="{'border-red-300': errors.name}"
                />
                <p v-if="errors.name" class="text-red-500 text-[10px] font-bold uppercase tracking-tight">{{ errors.name }}</p>
              </div>
              <div class="space-y-2">
                <label class="text-xs font-bold text-stone-400 uppercase tracking-widest">{{ currentLang === 'en' ? 'Email Address' : (currentLang === 'zh' ? '电子邮箱' : '電子郵箱') }}</label>
                <input 
                  v-model="form.email"
                  type="email" 
                  class="w-full px-5 py-4 bg-stone-50 border border-stone-200 rounded-2xl focus:outline-none focus:ring-2 focus:ring-emerald-500/20 focus:border-emerald-500 transition-all"
                  :class="{'border-red-300': errors.email}"
                />
                <p v-if="errors.email" class="text-red-500 text-[10px] font-bold uppercase tracking-tight">{{ errors.email }}</p>
              </div>
            </div>

            <div class="space-y-2">
              <label class="text-xs font-bold text-stone-400 uppercase tracking-widest">{{ currentLang === 'en' ? 'Subject' : (currentLang === 'zh' ? '主题' : '主題') }}</label>
              <input 
                v-model="form.subject"
                type="text" 
                class="w-full px-5 py-4 bg-stone-50 border border-stone-200 rounded-2xl focus:outline-none focus:ring-2 focus:ring-emerald-500/20 focus:border-emerald-500 transition-all"
              />
            </div>

            <div class="space-y-2">
              <label class="text-xs font-bold text-stone-400 uppercase tracking-widest">{{ currentLang === 'en' ? 'Your Message' : (currentLang === 'zh' ? '您的留言' : '您的留言') }}</label>
              <textarea 
                v-model="form.message"
                rows="5" 
                class="w-full px-5 py-4 bg-stone-50 border border-stone-200 rounded-2xl focus:outline-none focus:ring-2 focus:ring-emerald-500/20 focus:border-emerald-500 transition-all resize-none"
                :class="{'border-red-300': errors.message}"
              ></textarea>
              <p v-if="errors.message" class="text-red-500 text-[10px] font-bold uppercase tracking-tight">{{ errors.message }}</p>
            </div>

            <button 
              type="submit" 
              :disabled="isSubmitting"
              class="w-full py-5 bg-emerald-600 text-white rounded-2xl font-bold text-lg hover:bg-emerald-500 transition-all flex items-center justify-center space-x-3 disabled:opacity-50"
            >
              <span v-if="!isSubmitting">{{ currentLang === 'en' ? 'Send Message' : (currentLang === 'zh' ? '发送留言' : '發送留言') }}</span>
              <span v-else>{{ currentLang === 'en' ? 'Sending...' : (currentLang === 'zh' ? '发送中...' : '發送中...') }}</span>
              <Send v-if="!isSubmitting" class="w-5 h-5" />
            </button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>
