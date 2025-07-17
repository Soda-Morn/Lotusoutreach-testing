<template>
  <div class="container mx-auto px-6 py-12">
    <button @click="goBack"
            class="flex items-center text-black hover:text-pink-500 transition-colors duration-200 mb-6">
            <i class="fas fa-arrow-left mr-2"></i> Back to Programs
          </button>
    <div v-if="program">
      <img
        :src="program.image"
        :alt="program.title"
        class="w-full h-full object-cover"
      />
      <h1 class="text-3xl font-bold text-blue-700 mb-4">{{ program.title }}</h1>
      <p class="text-gray-700 text-lg leading-relaxed">{{ program.content }}</p>
    </div>
    <div v-else class="text-center text-gray-500">Loading program details...</div>
  </div>
</template>

<script setup>
import { useRoute, useRouter } from 'vue-router'
import { ref } from 'vue'

const route = useRoute()
const router = useRouter()

// ✅ Use either of these:
// const goBack = () => router.back() // ← Back to previous page
const goBack = () => router.push('/') // ← Back to specific route
// Sample program data
const programs = [
  {
    id: 1,
    title: 'Education in Cambodia',
    image: 'https://lotusoutreachaustralia.org.au/wp-content/uploads/2015/07/banner-photo-outside-house.jpg',
    content:`Lotus Outreach Cambodia supports girls in rural areas by providing scholarships, school supplies, uniforms, and nutritious meals. These efforts help remove financial barriers so girls can continue their education and build brighter futures.`

  },
  {
    id: 2,
    title: 'Healthcare Access',
    image: 'https://www.globalgiving.org/pfil/69718/pict_large.jpg',
    content:  `We bring essential healthcare services to remote communities, including mobile clinics and health education. Clean water projects improve health and reduce waterborne diseases, helping families live healthier lives.`
  },
  {
    id: 3,
    title: 'Anti-Trafficking Protection',
    image: 'https://www.globalgiving.org/pfil/5863/ph_5863_18888.jpg',
    content: `Our anti-trafficking programs focus on community education, economic empowerment, and support for survivors. We work with local partners to provide skills training and safe opportunities that reduce vulnerability to trafficking.`
  },
  {
    id: 4,
    title: 'Rural Development',
    image: 'https://lotusoutreach.org/wp-content/uploads/2019/01/26435170859_e94f24584d_o-1-e1547985152808.jpg',
    content:`We partner with communities to build vital infrastructure like clean water wells and support sustainable agriculture. Our programs create jobs and improve livelihoods, helping families thrive in rural Cambodia.`
  }
]

// Get the ID from the route, convert to number
const programId = parseInt(route.params.id)
const program = ref(programs.find(p => p.id === programId))
</script>
