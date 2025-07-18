<template>
  <div class="bg-white">
    <!-- Hero Banner Component -->
    <div class="relative min-h-screen bg-gray-100 overflow-hidden">
      <!-- Background Image -->
      <div class="absolute inset-0 overflow-hidden">
        <img
          src="https://lotusoutreachaustralia.org.au/wp-content/uploads/2020/03/Bondi-BH-Class-Donation-Poster.jpg"
          alt="Lotus Outreach activities"
          class="w-full h-full object-cover blur-sm"
        />
        <div class="absolute inset-0 bg-black/10"></div>
      </div>

      <!-- Content Overlay -->
      <div
        class="relative z-10 flex items-center justify-center min-h-screen px-4 sm:px-6 lg:px-8"
      >
        <div class="text-center max-w-3xl mx-auto">
          <h1
            class="text-4xl md:text-5xl lg:text-6xl font-bold text-white mb-4 leading-tight"
          >
            <span
              class="inline-block transform transition-all duration-500 hover:scale-105"
            >
              Empowering Communities
            </span>
            <br />
            <span
              class="inline-block transition-all duration-300 text-pink-400"
            >
              In Cambodia Through Sustainable Action
            </span>
          </h1>
          <p class="text-lg md:text-xl text-white mb-8 max-w-2xl mx-auto">
            Discover our ongoing activities and initiatives creating lasting
            change through education, sports, and community development across
            Cambodia.
          </p>
          <div class="flex flex-wrap justify-center gap-4">
            <button
              class="px-6 py-3 bg-pink-500 text-white font-medium rounded-full transition-all duration-300 shadow-lg hover:shadow-xl transform hover:-translate-y-1"
            >
              Our Programs
            </button>
            <button
              class="px-6 py-3 border-2 border-white text-white font-medium rounded-full hover:bg-white hover:text-gray-900 transition-all duration-300 transform hover:-translate-y-1"
            >
              Get Involved
            </button>
          </div>
        </div>
      </div>
    </div>
    <!-- Activities Listing View -->
    <div
      v-if="currentView === 'listing'"
      class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-16"
    >
      <!-- Header with Search -->
      <div class="text-center mb-12">
        <h2 class="text-3xl md:text-4xl font-bold text-gray-900 mb-3">
          Our Activities
        </h2>
        <p class="text-lg text-gray-600 max-w-2xl mx-auto mb-6">
          Explore our ongoing initiatives and programs making a difference in
          communities across Cambodia.
        </p>
        <!-- Search Bar -->
        <div class="max-w-md mx-auto relative">
          <div class="relative">
            <input
              v-model="searchQuery"
              type="text"
              placeholder="Search activities..."
              class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 outline-none transition-all duration-200 pr-10"
              @input="handleSearch"
            />
            <svg
              class="absolute right-3 top-3.5 h-5 w-5 text-gray-400"
              fill="none"
              stroke="currentColor"
              viewBox="0 0 24 24"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"
              ></path>
            </svg>
          </div>
          <!-- Category Filter -->
          <div class="flex flex-wrap justify-center gap-2 mt-4">
            <button
              v-for="category in categories"
              :key="category.value"
              @click="toggleCategory(category.value)"
              class="px-3 py-1 text-sm rounded-full transition-colors"
              :class="getCategoryButtonClass(category.value)"
            >
              {{ category.label }}
            </button>
          </div>
        </div>
      </div>
      <!-- No Results Message -->
      <div v-if="filteredActivities.length === 0" class="text-center py-12">
        <svg
          class="mx-auto h-12 w-12 text-gray-400"
          fill="none"
          stroke="currentColor"
          viewBox="0 0 24 24"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"
          ></path>
        </svg>
        <h3 class="mt-2 text-lg font-medium text-gray-900">
          No activities found
        </h3>
        <p class="mt-1 text-gray-500">
          Try adjusting your search or filter to find what you're looking for.
        </p>
        <button
          @click="resetFilters"
          class="mt-4 px-4 py-2 bg-blue-600 text-white rounded-md hover:bg-blue-700 transition-colors"
        >
          Reset filters
        </button>
      </div>
      <!-- Activities Grid -->
      <div v-else class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
        <article
          v-for="(activity, index) in filteredActivities.slice(0, visibleItems)"
          :key="index"
          class="group bg-white rounded-xl shadow-md overflow-hidden hover:shadow-lg transition-shadow duration-300 h-full flex flex-col"
        >
          <!-- Image Section -->
          <div class="h-48 overflow-hidden">
            <img
              :src="activity.image || '/placeholder.svg'"
              :alt="activity.title"
              class="w-full h-full object-cover transition-transform duration-500 group-hover:scale-105"
            />
          </div>
          <div class="p-6 md:p-8 flex-grow">
            <!-- Category Badge and Date -->
            <div class="flex items-center justify-between mb-4">
              <span
                class="inline-block px-3 py-1 text-xs font-semibold rounded-full"
                :class="getCategoryBadgeClass(activity.category)"
              >
                {{ getCategoryLabel(activity.category) }}
              </span>
              <span class="text-sm text-gray-500">{{
                formatDate(activity.date)
              }}</span>
            </div>
            <!-- Title -->
            <h3
              class="text-xl font-bold text-gray-900 mb-3 group-hover:text-blue-600 transition-colors"
            >
              {{ activity.title }}
            </h3>
            <!-- Location -->
            <p v-if="activity.location" class="text-sm text-gray-500 mb-2">
              📍 {{ activity.location }}
            </p>
            <!-- Content Preview -->
            <p class="text-gray-600 mb-4 line-clamp-3">
              {{ activity.content }}
            </p>
            <!-- Author -->
            <div class="mt-auto">
              <span class="text-sm font-medium text-gray-500"
                >By {{ activity.author }}</span
              >
            </div>
          </div>
          <!-- Learn More Button -->
          <div class="px-6 pb-6 md:px-8">
            <button
              class="w-full px-4 py-2 bg-blue-50 text-blue-600 rounded-md hover:bg-blue-100 transition-colors flex items-center justify-center"
              @click="viewActivityDetail(activity)"
            >
              Learn more
              <svg
                class="w-4 h-4 ml-1"
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
            </button>
          </div>
        </article>
      </div>
      <!-- Load More Button -->
      <div
        v-if="filteredActivities.length > visibleItems"
        class="mt-12 text-center"
      >
        <button
          @click="loadMore"
          class="px-6 py-3 bg-white border border-gray-300 rounded-md text-gray-700 font-medium hover:bg-gray-50 transition-colors"
        >
          Load More Activities
        </button>
      </div>
    </div>
    <!-- Activity Detail View -->
    <div
      v-if="currentView === 'detail' && selectedActivity"
      class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 py-8"
    >
      <!-- Back Button -->
      <button
        @click="backToListing"
        class="flex items-center space-x-2 text-gray-600 hover:text-gray-800 mb-6 transition-colors"
      >
        <svg
          class="w-5 h-5"
          fill="none"
          stroke="currentColor"
          viewBox="0 0 24 24"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M15 19l-7-7 7-7"
          />
        </svg>
        <span>Back to Activities</span>
      </button>
      <article class="bg-white rounded-xl shadow-sm overflow-hidden">
        <!-- Hero Image -->
        <div class="aspect-video overflow-hidden">
          <img
            :src="selectedActivity.image || '/placeholder.svg'"
            :alt="selectedActivity.title"
            class="w-full h-full object-cover"
          />
        </div>
        <!-- Article Content -->
        <div class="p-8">
          <!-- Article Header -->
          <div class="mb-6">
            <div class="flex items-center justify-between mb-4">
              <span
                class="px-3 py-1 text-sm font-medium rounded-full"
                :class="getCategoryBadgeClass(selectedActivity.category)"
              >
                {{ getCategoryLabel(selectedActivity.category) }}
              </span>
              <span class="text-sm text-gray-500">{{
                formatDate(selectedActivity.date)
              }}</span>
            </div>
            <h1 class="text-3xl md:text-4xl font-bold text-gray-900 mb-4">
              {{ selectedActivity.title }}
            </h1>
            <div class="flex items-center space-x-4 text-sm text-gray-500 mb-6">
              <span>By {{ selectedActivity.author }}</span>
              <span>•</span>
              <span
                >{{ calculateReadTime(selectedActivity.content) }} min
                read</span
              >
              <span v-if="selectedActivity.location">•</span>
              <span v-if="selectedActivity.location"
                >📍 {{ selectedActivity.location }}</span
              >
            </div>
          </div>
          <!-- Article Body -->
          <div class="prose prose-lg max-w-none">
            <div class="text-gray-700 leading-relaxed whitespace-pre-line">
              {{ selectedActivity.content }}
            </div>
          </div>
          <!-- Call to Action -->
          <div class="mt-8 p-6 bg-pink-50 rounded-lg text-center">
            <h3 class="text-xl font-bold text-gray-900 mb-2">
              Support Our Mission
            </h3>
            <p class="text-gray-600 mb-4">
              Help us continue empowering communities through education, health,
              and sustainable development in Cambodia.
            </p>
            <button
              class="bg-pink-600 text-white px-8 py-3 rounded-lg hover:bg-pink-700 transition-colors font-medium"
            >
              Get Involved Today
            </button>
          </div>
        </div>
      </article>
      <!-- Related Activities -->
      <div v-if="relatedActivities.length > 0" class="mt-12">
        <h3 class="text-2xl font-bold text-gray-900 mb-6">
          Related Activities
        </h3>
        <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
          <article
            v-for="activity in relatedActivities"
            :key="activity.title"
            class="bg-white rounded-lg shadow-sm overflow-hidden hover:shadow-md transition-shadow cursor-pointer"
            @click="viewActivityDetail(activity)"
          >
            <div class="flex">
              <div class="w-24 h-24 flex-shrink-0">
                <img
                  :src="activity.image || '/placeholder.svg'"
                  :alt="activity.title"
                  class="w-full h-full object-cover"
                />
              </div>
              <div class="p-4 flex-1">
                <h4 class="font-semibold text-gray-900 mb-1 line-clamp-2">
                  {{ activity.title }}
                </h4>
                <p class="text-sm text-gray-500">
                  {{ activity.author }} • {{ formatDate(activity.date) }}
                </p>
              </div>
            </div>
          </article>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";

// View state management
const currentView = ref("listing"); // 'listing' or 'detail'
const selectedActivity = ref(null);

// Reactive variables
const visibleItems = ref(6);
const searchQuery = ref("");
const activeCategories = ref([]);

const categories = [
  { value: "education", label: "Girls' Education" },
  { value: "health", label: "Health & Nutrition" },
  { value: "protection", label: "Anti-Trafficking & Child Protection" },
  { value: "livelihoods", label: "Sustainable Livelihoods" },
];

const activities = [
  {
    title: "Girls' Education Program Transforms Lives in Kampong Speu",
    content:
      "Our comprehensive program in Kampong Speu provides scholarships, school supplies, and mentorship to over 500 girls, ensuring they complete their primary and secondary education. We also run literacy classes for adult women, empowering entire families through learning. This initiative aims to break the cycle of poverty by providing access to quality education, which is often out of reach for families in remote areas. We work closely with local communities to identify needs and ensure our programs are culturally sensitive and effective. The long-term impact includes increased literacy rates, improved economic opportunities for women, and a more educated future generation.",
    date: "2024-07-10",
    author: "Education Team",
    category: "education",
    image: "https://csaf.org.kh/wp-content/uploads/2023/12/5-1024x683.jpg",
    location: "Kampong Speu, Cambodia",
  },
  {
    title: "Vital Health Services for Mothers and Children in Takeo",
    content:
      "In Takeo province, our mobile health clinics offer essential pre-natal care, safe delivery support, and post-natal check-ups. We also provide nutrition education and vaccinations for infants, significantly improving health outcomes in remote communities. Our teams travel to underserved areas, bringing critical medical services directly to those who need them most. This program addresses high rates of maternal and infant mortality by providing preventative care and health education, empowering mothers with the knowledge and resources to ensure their children's healthy development. We also train local health volunteers to sustain these efforts.",
    date: "2024-06-25",
    author: "Health Outreach Team",
    category: "health",
    image:" https://www.globalgiving.org/pfil/3885/Bikes_distribution_to_PNC_students_Large.jpg",
    location: "Takeo, Cambodia",
  },
  {
    title: "Combating Human Trafficking and Providing Safe Havens",
    content:
      "Based in Phnom Penh, this program focuses on preventing human trafficking through community awareness campaigns and providing immediate safe shelter, counseling, and legal aid to survivors, helping them rebuild their lives with dignity. We work tirelessly to identify and rescue victims, offering them a path to recovery and reintegration into society. Our approach includes working with law enforcement, community leaders, and families to create a strong protective network. Education on the dangers of trafficking is a key component, empowering vulnerable individuals to recognize and avoid exploitative situations.",
    date: "2024-06-18",
    author: "Protection Program",
    category: "protection",
    image: "https://www.globalgiving.org/pfil/3885/ph_3885_218251.jpg",
    location: "Phnom Penh, Cambodia",
  },
  {
    title: "Empowering Women Through Vocational Skills in Battambang",
    content:
      "Our center in Battambang offers vocational training in tailoring, weaving, and hospitality to vulnerable women, equipping them with marketable skills to secure employment and achieve financial independence for themselves and their families. This program is crucial for women who have limited educational opportunities, providing them with practical skills that lead directly to income generation. Beyond technical training, we also offer business literacy and life skills workshops, fostering confidence and self-reliance. Many graduates have successfully started their own small businesses or found stable employment, transforming their economic outlook.",
    date: "2024-06-05",
    author: "Livelihoods Team",
    category: "livelihoods",
    image: "https://www.globalgiving.org/pfil/3885/6989625829_7142fa33a8_z_Large.jpg",
    location: "Battambang, Cambodia",
  },
  {
    title: "Access to Clean Water Transforms Lives in Siem Reap",
    content:
      "This project in Siem Reap focuses on installing new water wells and implementing sanitation systems in rural villages. We also conduct hygiene education workshops to ensure long-term health benefits and sustainable community practices. Access to clean water is fundamental for health and development, reducing waterborne diseases and freeing up time for women and children who traditionally spend hours fetching water. Our approach involves community participation in the planning and maintenance of water infrastructure, ensuring sustainability and local ownership. This leads to healthier families and more time for education and productive activities.",
    date: "2024-05-28",
    author: "Community Development",
    category: "livelihoods",
    image: "https://b2616979.smushcdn.com/2616979/wp-content/uploads/Cambodia.10-2024.LisaHarbertson-253-scaled.jpg?lossy=2&strip=1&webp=1",
    location: "Siem Reap, Cambodia",
  },
  {
    title: "Creating Safe Environments for Children in Kandal",
    content:
      "In Kandal province, we establish and maintain safe playgrounds and community centers, providing children with secure spaces for learning and play. The program also includes workshops on child rights and protection for parents and local leaders. These safe spaces are vital for children's physical and emotional development, especially in areas where safe play is limited. We aim to foster a protective environment where children can thrive, free from harm and exploitation. Community engagement is key, as we empower parents and local authorities to become advocates for child protection and well-being.",
    date: "2024-05-15",
    author: "Child Protection Unit",
    category: "protection",
    image: "https://www.globalgiving.org/pfil/5863/ph_5863_18889.jpg",
    location: "Kandal, Cambodia",
  },
  {
    title: "Supporting Higher Education for Promising Students - Nationwide",
    content:
      "Our nationwide scholarship program identifies and supports talented students from disadvantaged backgrounds to pursue higher education. We cover tuition fees, living expenses, and provide mentorship, enabling them to become future leaders in Cambodia. This program is designed to bridge the gap for students who have the academic potential but lack the financial means to attend university. By investing in higher education, we are cultivating a new generation of professionals, innovators, and community leaders who will contribute to Cambodia's development. Our alumni network provides ongoing support and networking opportunities.",
    date: "2024-05-01",
    author: "Scholarship Committee",
    category: "education",
    image: "https://www.globalgiving.org/pfil/3885/ph_3885_218247.jpg",
    location: "Nationwide, Cambodia",
  },
];

// Computed properties
const filteredActivities = computed(() => {
  const query = searchQuery.value.toLowerCase().trim();
  const hasSearchQuery = query !== "";
  const hasActiveCategories = activeCategories.value.length > 0;

  return activities
    .filter((activity) => {
      const matchesCategory =
        !hasActiveCategories ||
        activeCategories.value.includes(activity.category);
      let matchesSearch = false;

      if (hasSearchQuery) {
        const matchedCategory = categories.find((cat) =>
          cat.label.toLowerCase().includes(query)
        );
        if (matchedCategory) {
          matchesSearch = activity.category === matchedCategory.value;
        } else {
          matchesSearch =
            activity.title.toLowerCase().includes(query) ||
            activity.content.toLowerCase().includes(query) ||
            activity.author.toLowerCase().includes(query) ||
            (activity.location &&
              activity.location.toLowerCase().includes(query));
        }
      } else {
        matchesSearch = true;
      }
      return matchesCategory && matchesSearch;
    })
    .sort((a, b) => new Date(b.date).getTime() - new Date(a.date).getTime());
});

const relatedActivities = computed(() => {
  if (!selectedActivity.value) return [];
  return activities
    .filter(
      (activity) =>
        activity.title !== selectedActivity.value.title &&
        (activity.category === selectedActivity.value.category ||
          Math.random() > 0.5) // Randomly show some from other categories
    )
    .slice(0, 2);
});

// Methods
const viewActivityDetail = (activity) => {
  selectedActivity.value = activity;
  currentView.value = "detail";
  window.scrollTo({ top: 0, behavior: "smooth" });
};

const backToListing = () => {
  currentView.value = "listing";
  selectedActivity.value = null;
  window.scrollTo({ top: 0, behavior: "smooth" });
};

const calculateReadTime = (content) => {
  const wordsPerMinute = 200;
  const wordCount = content.split(/\s+/).length;
  return Math.ceil(wordCount / wordsPerMinute);
};

const getCategoryButtonClass = (category) => {
  const isActive = activeCategories.value.includes(category);
  return {
    "bg-blue-100 text-blue-800": category === "education" && isActive,
    "bg-green-100 text-green-800": category === "health" && isActive,
    "bg-purple-100 text-purple-800": category === "protection" && isActive,
    "bg-orange-100 text-orange-800": category === "livelihoods" && isActive,
    "bg-gray-100 text-gray-800": !isActive,
  };
};

const getCategoryBadgeClass = (category) => {
  return {
    "bg-blue-100 text-blue-800": category === "education",
    "bg-green-100 text-green-800": category === "health",
    "bg-purple-100 text-purple-800": category === "protection",
    "bg-orange-100 text-orange-800": category === "livelihoods",
  };
};

const loadMore = () => {
  visibleItems.value += 3;
};

const handleSearch = () => {
  visibleItems.value = 6;
};

const toggleCategory = (category) => {
  const index = activeCategories.value.indexOf(category);
  if (index === -1) {
    activeCategories.value.push(category);
  } else {
    activeCategories.value.splice(index, 1);
  }
  visibleItems.value = 6;
};

const resetFilters = () => {
  searchQuery.value = "";
  activeCategories.value = [];
  visibleItems.value = 6;
};

const formatDate = (dateString) => {
  const options = { year: "numeric", month: "long", day: "numeric" };
  return new Date(dateString).toLocaleDateString("en-US", options);
};

const getCategoryLabel = (category) => {
  const labels = {
    education: "Girls' Education",
    health: "Health & Nutrition",
    protection: "Anti-Trafficking & Child Protection",
    livelihoods: "Sustainable Livelihoods",
  };
  return labels[category] || "Activity";
};
</script>

<style scoped>
/* Custom styles */
.line-clamp-3 {
  display: -webkit-box;
  -webkit-line-clamp: 3;
  line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}
.line-clamp-2 {
  display: -webkit-box;
  -webkit-line-clamp: 2;
  line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}
.prose {
  line-height: 1.75;
}
.prose p {
  margin-bottom: 1.25em;
}
/* Image styles */
.h-48 {
  height: 12rem;
}
.h-64 {
  height: 16rem;
}
.object-cover {
  object-fit: cover;
}
.aspect-video {
  aspect-ratio: 16 / 9;
}
/* Transition effects */
.transition-all {
  transition-property: all;
  transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
  transition-duration: 150ms;
}
</style>
