<template>
  <div v-if="program" class="min-h-screen">
    <!-- Full-screen background header with overlay -->
    <div
      class="relative h-screen bg-cover bg-center bg-no-repeat text-white"
      :style="{ backgroundImage: `url(${program.image})` }"
    >
      <div
        class="absolute inset-0 bg-gradient-to-t from-black/60 to-transparent"
      ></div>

      <div
        class="container mx-auto px-4 max-w-7xl relative z-10 h-full flex flex-col justify-end pb-20"
      >
        <button
          @click="goBack"
          class="group inline-flex items-center gap-2 bg-white/20 px-5 py-2 rounded-full text-white border border-white/30 hover:bg-pink-600 hover:text-white hover:border-pink-600 transition-all duration-300 shadow-lg backdrop-blur-sm mb-8 w-fit"
        >
          <ArrowLeftIcon
            class="w-4 h-4 group-hover:-translate-x-1 transition-transform duration-300"
          />
          <span class="font-semibold tracking-wide">Back to Programs</span>
        </button>

        <div class="flex items-center">
          <div
            class="w-16 h-16 rounded-full bg-blue-200/20 flex items-center justify-center mr-6"
          >
            <i class="fas fa-seedling text-2xl text-white"></i>
          </div>
          <div>
            <h1 class="text-3xl md:text-5xl font-poppins font-semibold mb-2">
              {{ program.title }}
            </h1>
            <p class="text-base md:text-lg text-white/90 max-w-2xl">
              {{ program.content }}
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>

  <div v-else class="text-center text-gray-500 py-12">
    Loading program details...
  </div>
</template>

<script setup>
import { useRoute, useRouter } from "vue-router";
import { ref } from "vue";

const route = useRoute();
const router = useRouter();

// ✅ Use either of these:
// const goBack = () => router.back() // ← Back to previous page
const goBack = () => router.push("/"); // ← Back to specific route
// Sample program data
const programs = [
  {
    id: 1,
    title: "Education in Cambodia",
    image:
      "https://lotusoutreachaustralia.org.au/wp-content/uploads/2015/07/banner-photo-outside-house.jpg",
    content: `Lotus Outreach Cambodia supports girls in rural areas by providing scholarships, school supplies, uniforms, and nutritious meals. These efforts help remove financial barriers so girls can continue their education and build brighter futures.`,
  },
  {
    id: 2,
    title: "Healthcare Access",
    image: "https://www.globalgiving.org/pfil/69718/pict_large.jpg",
    content: `We bring essential healthcare services to remote communities, including mobile clinics and health education. Clean water projects improve health and reduce waterborne diseases, helping families live healthier lives.`,
  },
  {
    id: 3,
    title: "Anti-Trafficking Protection",
    image: "https://www.globalgiving.org/pfil/5863/ph_5863_18888.jpg",
    content: `Our anti-trafficking programs focus on community education, economic empowerment, and support for survivors. We work with local partners to provide skills training and safe opportunities that reduce vulnerability to trafficking.`,
  },
  {
    id: 4,
    title: "Rural Development",
    image:
      "https://lotusoutreach.org/wp-content/uploads/2019/01/26435170859_e94f24584d_o-1-e1547985152808.jpg",
    content: `We partner with communities to build vital infrastructure like clean water wells and support sustainable agriculture. Our programs create jobs and improve livelihoods, helping families thrive in rural Cambodia.`,
  },
];

// Get the ID from the route, convert to number
const programId = parseInt(route.params.id);
const program = ref(programs.find((p) => p.id === programId));
</script>
