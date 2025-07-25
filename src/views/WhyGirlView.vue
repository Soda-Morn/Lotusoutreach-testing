<template>
  <div class="min-h-screen bg-white">
    <!-- Hero Section with Slideshow -->
    <section class="relative h-screen overflow-hidden">
      <div class="absolute inset-0">
        <div
          class="flex h-full transition-transform duration-700 ease-in-out"
          :style="{ transform: `translateX(-${currentSlide * 100}%)` }"
        >
          <div
            v-for="(image, index) in heroImages"
            :key="index"
            class="w-full h-full flex-shrink-0 relative"
          >
            <img
              :src="image.src"
              :alt="image.alt"
              class="w-full h-full object-cover"
            />
            <div
              class="absolute inset-0 bg-gradient-to-r from-black/70 via-black/50 to-transparent"
            ></div>
          </div>
        </div>
      </div>

      <!-- Hero Content -->
      <div class="relative z-10 h-full flex items-center">
        <div class="container mx-auto px-6 lg:px-8">
          <div class="max-w-3xl">
            <h1
              class="text-5xl lg:text-7xl font-bold text-white mb-6 leading-tight"
            >
              Empowering <span class="text-pink-400">Cambodia's</span> Girls
            </h1>
            <p class="text-xl lg:text-2xl text-gray-200 mb-8 leading-relaxed">
              In rural Cambodia, education transforms lives. When you empower a
              Cambodian girl, you transform an entire community.
            </p>
            <div class="flex flex-col sm:flex-row gap-4">
              <button
                @click="navigateTo('/donate')"
                class="px-8 py-4 bg-pink-600 hover:bg-pink-700 text-white font-semibold rounded-full transition-all duration-300 transform hover:scale-105 shadow-lg"
              >
                Support Cambodia
              </button>
              <button
                @click="navigateTo('/cambodia')"
                class="px-8 py-4 border-2 border-white text-white hover:bg-white hover:text-gray-900 font-semibold rounded-full transition-all duration-300"
              >
                Learn About Our Work
              </button>
            </div>
          </div>
        </div>
      </div>

      <!-- Slide Indicators -->
      <div
        class="absolute bottom-8 left-1/2 transform -translate-x-1/2 flex space-x-2 z-20"
      >
        <button
          v-for="(image, index) in heroImages"
          :key="index"
          @click="currentSlide = index"
          class="w-2 h-2 rounded-full transition-all duration-300"
          :class="
            currentSlide === index
              ? 'bg-white scale-125'
              : 'bg-white/50 hover:bg-white/75'
          "
        ></button>
      </div>
    </section>

    <!-- Impact Statistics -->
    <section
      ref="statisticsRef"
      class="py-20 bg-gradient-to-r from-blue-50 to-pink-50"
    >
      <div class="container mx-auto px-6">
        <div class="text-center mb-12">
          <h2 class="text-3xl font-bold text-gray-900 mb-4">
            Our Impact in Cambodia
          </h2>
          <p class="text-lg text-gray-600">
            Transforming lives across rural Cambodian communities
          </p>
        </div>
        <div class="grid grid-cols-1 md:grid-cols-3 gap-8 text-center">
          <div class="group">
            <div
              :class="[
                'text-5xl font-bold mb-2 group-hover:scale-110 transition-transform duration-300',
                counters.children.color,
              ]"
            >
              {{
                formatNumber(
                  counters.children.current,
                  counters.children.target,
                  counters.children.suffix
                )
              }}
            </div>
            <p class="text-gray-700 font-medium">
              Cambodian children supported through education
            </p>
          </div>
          <div class="group">
            <div
              :class="[
                'text-5xl font-bold mb-2 group-hover:scale-110 transition-transform duration-300',
                counters.villagers.color,
              ]"
            >
              {{
                formatNumber(
                  counters.villagers.current,
                  counters.villagers.target,
                  counters.villagers.suffix
                )
              }}
            </div>
            <p class="text-gray-700 font-medium">
              Rural families with access to clean water
            </p>
          </div>
          <div class="group">
            <div
              :class="[
                'text-5xl font-bold mb-2 group-hover:scale-110 transition-transform duration-300',
                counters.years.color,
              ]"
            >
              {{
                formatNumber(
                  counters.years.current,
                  counters.years.target,
                  counters.years.suffix
                )
              }}
            </div>
            <p class="text-gray-700 font-medium">
              Years serving Cambodia's communities
            </p>
          </div>
        </div>
      </div>
    </section>

    <!-- Mission Cards -->
    <section class="py-20">
      <div class="container mx-auto px-6">
        <div class="text-center mb-16">
          <h2 class="text-4xl font-bold text-gray-900 mb-4">
            Transforming Cambodia
          </h2>
          <p class="text-xl text-gray-600 max-w-3xl mx-auto">
            We work in the most remote provinces of Cambodia, providing
            education, healthcare, and community development programs.
          </p>
        </div>

        <!-- Constrain width to match navbar content -->
        <div class="max-w-7xl mx-auto">
          <div class="grid grid-cols-1 lg:grid-cols-2 gap-8">
            <!-- Empowerment Card -->
            <div
              class="group relative overflow-hidden rounded-2xl shadow-xl hover:shadow-2xl transition-all duration-500"
            >
              <div class="aspect-[4/3] overflow-hidden">
                <img
                  src="https://www.globalgiving.org/pfil/5863/pict_large.jpg"
                  alt="Cambodian girls in education"
                  class="w-full h-full object-cover group-hover:scale-110 transition-transform duration-700"
                />
              </div>
              <div
                class="absolute inset-0 bg-gradient-to-t from-black/80 via-black/20 to-transparent"
              ></div>
              <div class="absolute bottom-0 left-0 right-0 p-8 text-white">
                <h3 class="text-2xl font-bold mb-3">
                  Education Opens Doors in Rural Cambodia
                </h3>
                <p class="text-gray-200 leading-relaxed">
                  In Cambodia's remote villages, we provide scholarships, school
                  supplies, and support systems that keep girls in school and
                  break cycles of poverty.
                </p>
              </div>
            </div>

            <!-- Global Impact Card -->
            <div
              class="group relative overflow-hidden rounded-2xl shadow-xl hover:shadow-2xl transition-all duration-500"
            >
              <div class="aspect-[4/3] overflow-hidden">
                <img
                  src="https://www.globalgiving.org/learn/wp-content/uploads/2022/10/Globalteer.jpg"
                  alt="Cambodian community"
                  class="w-full h-full object-cover group-hover:scale-110 transition-transform duration-700"
                />
              </div>
              <div
                class="absolute inset-0 bg-gradient-to-t from-black/80 via-black/20 to-transparent"
              ></div>
              <div class="absolute bottom-0 left-0 right-0 p-8 text-white">
                <h3 class="text-2xl font-bold mb-3 text-white">
                  Building Stronger Communities
                </h3>
                <!-- <p class="text-lg font-semibold mb-3">
                  Across Cambodia's rural provinces
                </p> -->
                <p class="text-gray-200 leading-relaxed">
                  Our comprehensive programs address the unique challenges
                  facing Cambodian families in Siem Reap, Battambang, and other
                  rural areas.
                </p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Focus Areas -->
    <section class="py-20 bg-gray-50">
      <div class="container mx-auto px-6">
        <div class="text-center mb-16">
          <h2 class="text-4xl font-bold text-gray-900 mb-4">
            Our Programs in Cambodia
          </h2>
          <p class="text-xl text-gray-600">
            Culturally-sensitive programs designed for Cambodian communities
          </p>
        </div>

        <!-- Constrain width to match navbar content -->
        <div class="max-w-7xl mx-auto">
          <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">
            <div
              v-for="card in focusCards"
              :key="card.id"
              class="bg-white rounded-xl shadow-lg hover:shadow-xl transition-all duration-300 overflow-hidden group cursor-pointer"
            >
              <router-link :to="`/education/${card.id}`" class="block">
                <div class="aspect-[4/3] overflow-hidden">
                  <img
                    :src="card.image"
                    :alt="card.title"
                    class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-500"
                  />
                </div>
                <div class="p-6">
                  <h3
                    class="text-xl font-bold text-blue-600 mb-3 group-hover:text-blue-700 transition-colors"
                  >
                    {{ card.title }}
                  </h3>
                  <p class="text-gray-600 mb-4 line-clamp-3">
                    {{ card.summary }}
                  </p>
                  <div
                    class="flex items-center text-pink-600 font-semibold group-hover:text-pink-700 transition-colors"
                  >
                    <span>Learn More</span>
                    <svg
                      class="w-4 h-4 ml-2 group-hover:translate-x-1 transition-transform"
                      fill="none"
                      stroke="currentColor"
                      viewBox="0 0 24 24"
                    >
                      <path
                        stroke-linecap="round"
                        stroke-linejoin="round"
                        stroke-width="2"
                        d="M9 5l7 7-7 7"
                      ></path>
                    </svg>
                  </div>
                </div>
              </router-link>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Our Approach -->
    <section class="py-20">
      <div class="container mx-auto px-6">
        <div class="max-w-7xl mx-auto">
          <div class="text-center mb-16">
            <h2 class="text-4xl font-bold text-gray-900 mb-4">
              Our Cambodia-Focused Approach
            </h2>
            <p class="text-xl text-gray-600">
              Understanding Khmer culture and community needs
            </p>
          </div>

          <div class="grid grid-cols-1 lg:grid-cols-2 gap-12 items-center">
            <!-- Image -->
            <div class="order-2 lg:order-1">
              <img
                src="https://images.globalgiving.org/pfil/3885/pict_original.jpg?w=460&h=306&auto=compress,enhance&fit=crop&crop=faces,center&format=auto&dpr=2"
                alt="Cambodian women and children"
                class="w-full h-96 object-cover rounded-2xl shadow-xl hover:shadow-2xl transition-shadow duration-300"
              />
            </div>

            <!-- Content -->
            <div class="order-1 lg:order-2">
              <!-- Tab Buttons -->
              <div class="grid grid-cols-2 gap-3 mb-8">
                <button
                  v-for="approach in approaches"
                  :key="approach.key"
                  @click="activeApproach = approach.key"
                  :class="[
                    'px-4 py-3 rounded-lg font-semibold transition-all duration-300 text-sm',
                    activeApproach === approach.key
                      ? 'bg-pink-600 text-white shadow-lg transform scale-105'
                      : 'bg-gray-100 text-gray-700 hover:bg-gray-200',
                  ]"
                >
                  {{ approach.title }}
                </button>
              </div>

              <!-- Tab Content -->
              <div
                class="bg-white p-8 rounded-xl shadow-lg border border-gray-100"
              >
                <div
                  v-for="approach in approaches"
                  :key="approach.key"
                  v-show="activeApproach === approach.key"
                  class="space-y-4"
                >
                  <h3 class="text-2xl font-bold text-gray-900 mb-4">
                    {{ approach.title }}
                  </h3>
                  <div class="prose prose-gray max-w-none">
                    <p
                      v-for="paragraph in approach.content"
                      :key="paragraph"
                      class="text-gray-700 leading-relaxed"
                    >
                      {{ paragraph }}
                    </p>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Water Initiative -->
    <section class="py-20 bg-gradient-to-br from-blue-50 via-white to-blue-50">
      <div class="container mx-auto px-6">
        <div class="max-w-6xl mx-auto">
          <div class="grid grid-cols-1 lg:grid-cols-2 gap-12 items-center">
            <!-- Content -->
            <div class="space-y-6">
              <div
                class="inline-block w-16 h-1 bg-blue-500 rounded-full mb-4"
              ></div>
              <h3 class="text-4xl font-bold text-blue-700 leading-tight">
                Clean Water for Cambodia's Villages
              </h3>
              <p class="text-xl text-gray-700 leading-relaxed">
                In rural Cambodia, access to clean water transforms entire
                communities.
                <span class="font-semibold text-blue-600"
                  >Over 70% of rural Cambodian families</span
                >
                still lack reliable access to safe drinking water.
              </p>

              <div
                class="bg-white p-6 rounded-xl shadow-lg border-l-4 border-blue-500"
              >
                <div class="text-center">
                  <div class="text-4xl font-bold text-blue-600 mb-2">150+</div>
                  <p class="text-gray-800 font-medium">
                    Water wells built in Cambodian villages since 2010
                  </p>
                </div>
              </div>
            </div>

            <!-- Image -->
            <div>
              <img
                src="https://lotusoutreach.org/wp-content/uploads/2018/12/people_at_public_water_pump.jpg"
                alt="Cambodian villagers at water pump"
                class="w-full h-96 object-cover rounded-2xl shadow-xl hover:shadow-2xl transition-shadow duration-300"
              />
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Call to Action -->
    <section class="relative py-20 overflow-hidden">
      <!-- Background Image -->
      <div class="absolute inset-0">
        <img
          src="https://images.globalgiving.org/pfil/10626/pict_original.jpg?w=460&h=306&auto=compress,enhance&fit=crop&crop=faces,center&format=auto&dpr=2"
          alt="Cambodia background"
          class="w-full h-full object-cover"
        />
        <!-- Dark Overlay -->
        <div class="absolute inset-0 bg-black/60"></div>
      </div>

      <!-- Content -->
      <div class="relative z-10 container mx-auto px-6 text-center">
        <div class="max-w-4xl mx-auto">
          <div class="mb-8">
            <svg
              class="h-16 w-16 mx-auto mb-6 text-white"
              fill="none"
              stroke="currentColor"
              viewBox="0 0 24 24"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M13 10V3L4 14h7v7l9-11h-7z"
              ></path>
            </svg>
          </div>
          <blockquote
            class="text-2xl lg:text-3xl font-medium text-white leading-relaxed mb-8"
          >
            "Education for Cambodia's girls is the foundation for the country's
            sustainable development and economic growth."
          </blockquote>
          <button
            class="px-10 py-4 bg-white text-pink-600 font-bold rounded-full hover:bg-gray-100 transition-colors duration-300 transform hover:scale-105 shadow-lg"
          >
            Support Cambodia Today
          </button>
        </div>
      </div>
    </section>

    <!-- Modal -->
    <div
      v-if="selectedCard"
      class="fixed inset-0 bg-black/75 flex items-center justify-center z-50 p-4"
      @click="closeModal"
    >
      <div
        class="bg-white rounded-2xl shadow-2xl max-w-2xl w-full max-h-[90vh] overflow-y-auto"
        @click.stop
      >
        <div class="relative">
          <img
            :src="selectedCard.image"
            :alt="selectedCard.title"
            class="w-full h-65 object-cover rounded-t-2xl"
          />
          <button
            @click="closeModal"
            class="absolute top-4 right-4 w-10 h-10 bg-white/90 hover:bg-white rounded-full flex items-center justify-center text-gray-600 hover:text-gray-900 transition-colors"
          >
            <svg
              class="w-6 h-6"
              fill="none"
              stroke="currentColor"
              viewBox="0 0 24 24"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M6 18L18 6M6 6l12 12"
              ></path>
            </svg>
          </button>
        </div>
        <div class="p-8">
          <h2 class="text-3xl font-bold text-pink-600 mb-6">
            {{ selectedCard.title }}
          </h2>
          <div class="prose prose-gray max-w-none">
            <p class="text-gray-700 leading-relaxed whitespace-pre-line">
              {{ selectedCard.content }}
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { Navigation } from "lucide-vue-next";
import { ref, onMounted, onUnmounted } from "vue";
// import { ref } from 'vue'
import { useRoute, useRouter } from "vue-router";

const mobileMenuOpen = ref(false);
const route = useRoute();
const router = useRouter();

const isActive = (path) => {
  return route.path === path;
};

const navigateTo = (path) => {
  router.push(path);
};

// / Full program list (same as in the list view)
const focusCards = [
  {
    id: 1,
    title: "Education in Cambodia",
    image: "https://lotusoutreachaustralia.org.au/wp-content/uploads/2015/07/banner-photo-outside-house.jpg",
    summary: "Supporting Cambodian girls through scholarships, school supplies, and educational programs in rural provinces.",
    content: "Our education programs in Cambodia focus on keeping girls in school through comprehensive support including scholarships, uniforms, school supplies, and nutritional assistance..."
  },
  {
    id: 2,
    title: "Healthcare Access",
    image: "https://www.globalgiving.org/pfil/69718/pict_large.jpg",
    summary: "Providing essential healthcare services and clean water access to remote Cambodian villages.",
    content: "In Cambodia's remote areas, we provide mobile health clinics, maternal health services, and health education programs..."
  },
  {
    id: 3,
    title: "Anti-Trafficking Protection",
    image: "https://www.globalgiving.org/pfil/5863/ph_5863_18888.jpg",
    summary: "Protecting vulnerable Cambodian women and children from trafficking and exploitation.",
    content: "Cambodia faces unique challenges with human trafficking, particularly affecting young women and children..."
  },
  {
    id: 4,
    title: "Rural Development",
    image: "https://lotusoutreach.org/wp-content/uploads/2019/01/26435170859_e94f24584d_o-1-e1547985152808.jpg",
    summary: "Building sustainable infrastructure and economic opportunities in Cambodia's rural communities.",
    content: "Our community development programs in Cambodia focus on building essential infrastructure like water wells, improving agricultural practices..."
  }
]

// Hero slideshow state
const currentSlide = ref(0);
const slideInterval = ref(null);

const heroImages = ref([
  {
    src: "https://business-cambodia.com/cms/assets/2f22a1db-85ee-42e9-8a8c-a0a134e1a82c",
    alt: "Cambodian Community Group",
  },
  {
    src: "https://lotusoutreach.org/wp-content/uploads/2018/12/Girls-Access-to-Education-1.jpg",
    alt: "Cambodian Girls in Education",
  },
  {
    src: "https://media.licdn.com/dms/image/v2/C561BAQHovERV7NaR7g/company-background_10000/company-background_10000/0/1615466141859/lotusoutreachinternational_cover?e=2147483647&v=beta&t=E2rwHcaKf0iDwP57SpCCBdOm12F61_c_-Pd5g8VQ8kg",
    alt: "Cambodian Children and Families",
  },
]);

// Modal state
const selectedCard = ref(null);

// Approach tabs state
const activeApproach = ref("culturally-sensitive");

const approaches = ref([
  {
    key: "culturally-sensitive",
    title: "Culturally Sensitive",
    content: [
      "Our programs in Cambodia are designed with deep respect for Khmer culture, Buddhist traditions, and local customs. We work closely with village elders, monks, and community leaders to ensure our initiatives align with cultural values while promoting positive change.",
      "Understanding the importance of family honor and community harmony in Cambodian society, we approach sensitive topics like girls' education and women's empowerment with cultural sensitivity and patience, building trust over time.",
    ],
  },
  {
    key: "locally-led",
    title: "Locally Led",
    content: [
      "Our Cambodia operations are led by Cambodian staff who understand the language, culture, and specific challenges facing rural communities. This local leadership ensures our programs are relevant, effective, and sustainable.",
      "We prioritize hiring and training Cambodian team members, creating local employment while building capacity within communities. Our approach empowers Cambodians to lead their own development initiatives.",
    ],
  },
  {
    key: "community-based",
    title: "Community Based",
    content: [
      "Every program begins with extensive community consultation. We work with village committees, women's groups, and local leaders to identify priorities and design solutions that reflect community needs and values.",
      "Our community-based approach ensures that programs are owned and sustained by the communities themselves, creating lasting change that continues long after our direct involvement ends.",
    ],
  },
  {
    key: "holistic",
    title: "Holistic Approach",
    content: [
      "We recognize that challenges in rural Cambodia are interconnected. Poverty, lack of education, health issues, and limited economic opportunities all affect each other. Our programs address multiple issues simultaneously for maximum impact.",
      "By combining education support with health services, clean water access, and economic opportunities, we create comprehensive solutions that address root causes of poverty and inequality in Cambodian communities.",
    ],
  },
]);

// Animated counters state
const counters = ref({
  children: { current: 0, target: 5000, suffix: "+", color: "text-blue-600" },
  villagers: { current: 0, target: 25000, suffix: "+", color: "text-pink-600" },
  years: { current: 0, target: 25, suffix: "+", color: "text-purple-600" },
});

const statisticsRef = ref(null);
const hasAnimated = ref(false);

// Counter animation methods
const formatNumber = (num, target, suffix) => {
  if (target >= 1000) {
    return (num / 1000).toFixed(0) + "K" + suffix.replace("+", "+");
  } else {
    return num + suffix;
  }
};

const animateCounter = (key, duration = 2000) => {
  const counter = counters.value[key];
  const startTime = Date.now();
  const startValue = counter.current;

  const animate = () => {
    const elapsed = Date.now() - startTime;
    const progress = Math.min(elapsed / duration, 1);

    // Easing function for smooth animation
    const easeOutQuart = 1 - Math.pow(1 - progress, 4);

    counter.current = Math.floor(
      startValue + (counter.target - startValue) * easeOutQuart
    );

    if (progress < 1) {
      requestAnimationFrame(animate);
    } else {
      counter.current = counter.target;
    }
  };

  requestAnimationFrame(animate);
};

const startCounterAnimations = () => {
  if (hasAnimated.value) return;

  hasAnimated.value = true;
  animateCounter("children", 2500);
  setTimeout(() => animateCounter("villagers", 2000), 200);
  setTimeout(() => animateCounter("years", 1500), 400);
};

const checkScrollPosition = () => {
  if (!statisticsRef.value || hasAnimated.value) return;

  const rect = statisticsRef.value.getBoundingClientRect();
  const isVisible = rect.top < window.innerHeight && rect.bottom > 0;

  if (isVisible) {
    startCounterAnimations();
  }
};

// Methods
const startAutoSlide = () => {
  slideInterval.value = setInterval(() => {
    currentSlide.value = (currentSlide.value + 1) % heroImages.value.length;
  }, 6000);
};

const openModal = (card) => {
  selectedCard.value = card;
  document.body.style.overflow = "hidden";
};

const closeModal = () => {
  selectedCard.value = null;
  document.body.style.overflow = "";
};

// Lifecycle
onMounted(() => {
  startAutoSlide();
  window.addEventListener("scroll", checkScrollPosition);
  checkScrollPosition(); // Check initial position
});

onUnmounted(() => {
  if (slideInterval.value) {
    clearInterval(slideInterval.value);
  }
  window.removeEventListener("scroll", checkScrollPosition);
  document.body.style.overflow = "";
});
</script>

<style scoped>
.line-clamp-3 {
  display: -webkit-box;
  -webkit-line-clamp: 3;
  line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.prose p {
  margin-bottom: 1rem;
}
</style>
