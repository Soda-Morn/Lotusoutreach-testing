<template>
  <div v-if="program" class="min-h-screen">
    <!-- Full-screen background header with overlay -->
    <div
      class="relative h-screen bg-cover object-contain bg-no-repeat text-white"
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
          class="group items-center gap-2 bg-white/20 px-5 py-2 rounded-full text-white border border-white/30 hover:bg-pink-600 hover:text-white hover:border-pink-600 transition-all duration-300 shadow-lg backdrop-blur-sm mb-8 ml-20 w-fit"
        >
          <ArrowLeftIcon
            class="w-4 h-4 group-hover:-translate-x-1 transition-transform duration-300"
          />
          <span class="font-semibold tracking-wide">Back to MyGirl</span>
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
              {{ program.summary }}
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
  <div
    v-for="(section, index) in program.contents"
    :key="index"
    class="px-4 md:px-8 py-10 max-w-4xl mx-auto text-gray-700"
  >
    <h2 class="text-2xl md:text-3xl font-semibold text-gray-800 mb-4">
      {{ section.title }}
    </h2>
    <p class="text-base md:text-lg leading-relaxed whitespace-pre-line">
      {{ section.content }}
    </p>
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
    summary: `Lotus Outreach Cambodia supports girls in rural areas by providing scholarships, school supplies, uniforms, and nutritious meals. These efforts help remove financial barriers so girls can continue their education and build brighter futures.`,
    contents: [
      {
        title: "Education in Cambodia",
        content: `Lotus Outreach Cambodia is committed to empowering girls in rural and underserved communities by removing the key financial and social obstacles that prevent them from accessing quality education. Through its comprehensive support programs, the organization provides full scholarships, including tuition coverage, school supplies, uniforms, transportation support, and nutritious daily meals.
    Beyond basic educational access, Lotus Outreach ensures that families who might otherwise rely on their daughters for household income or labor receive monthly rice stipends, reducing economic pressure and encouraging long-term school attendance. The organization also offers bicycles to girls living far from school, ensuring safe and consistent access to education.
    By addressing both economic hardship and gender-based barriers, Lotus Outreach Cambodia helps girls not only stay in school, but also thrive academically, develop leadership skills, and build a foundation for a brighter, more independent future. These integrated efforts have transformed the lives of hundreds of young Cambodian women, empowering them to break the cycle of poverty for themselves and their communities.`,
      },
    ],
  },
  {
    id: 2,
    title: "Healthcare Access",
    image: "https://www.globalgiving.org/pfil/69718/pict_large.jpg",
    summary: `We bring essential healthcare services to remote communities, including mobile clinics and health education. Clean water projects improve health and reduce waterborne diseases, helping families live healthier lives.`,
    contents: [
      {
        title: "Healthcare Access",
        content: `Lotus Outreach Cambodia is deeply committed to improving the health and well-being of underserved populations in rural and remote communities. Recognizing that limited access to healthcare services significantly affects quality of life, we implement a multi-pronged approach to ensure that vulnerable families receive the care and support they need.
    Our mobile health clinics regularly travel to isolated villages, providing free medical check-ups, vaccinations, maternal care, and treatment for common illnesses. These clinics serve as a lifeline for families who would otherwise have to travel long distances and incur high costs to receive even basic care.
    We also prioritize health education, empowering communities with essential knowledge on hygiene, nutrition, reproductive health, disease prevention, and proper sanitation practices. These community workshops are especially impactful for women and children, equipping them to make informed decisions that lead to healthier lifestyles.`,
      },
    ],

  },
  {
    id: 3,
    title: "Anti-Trafficking Protection",
    image: "https://www.globalgiving.org/pfil/5863/ph_5863_18888.jpg",
    summary: `Our anti-trafficking programs focus on community education, economic empowerment, and support for survivors. We work with local partners to provide skills training and safe opportunities that reduce vulnerability to trafficking.`,
    contents: [
      {
        title: "Anti-Trafficking Protection",
        content: `Lotus Outreach Cambodia is dedicated to protecting vulnerable populations—especially women and children—from the dangers of human trafficking. Our Anti-Trafficking Protection programs take a comprehensive, community-centered approach that addresses both the causes and consequences of exploitation.
    We begin by focusing on community education and awareness, working directly with at-risk communities to raise understanding of trafficking risks, common tactics used by traffickers, and the importance of safe migration. Through workshops, school outreach, and informational campaigns, we help families make informed decisions and recognize early warning signs.
    To combat the economic pressures that often lead to exploitation, we provide economic empowerment programs such as vocational training, job placement assistance, and income-generating opportunities. These programs enable women and girls—who are especially vulnerable—to become financially independent, reducing their susceptibility to false promises of work or migration.
    For survivors of trafficking, we offer comprehensive reintegration support, including trauma counseling, legal assistance, safe shelter, and continued education or vocational training. By working with trusted local partners, we ensure that survivors receive the care they need to rebuild their lives with dignity and stability.
    Ultimately, our Anti-Trafficking Protection efforts aim not only to rescue and rehabilitate victims, but also to prevent trafficking before it occurs. Through empowerment, education, and sustainable development, we help create safer communities where every individual has the right and opportunity to live free from exploitation.`,
      },
    ],
  },
  {
    id: 4,
    title: "Rural Development",
    image:
      "https://lotusoutreach.org/wp-content/uploads/2019/01/26435170859_e94f24584d_o-1-e1547985152808.jpg",
    summary: `We partner with communities to build vital infrastructure like clean water wells and support sustainable agriculture. Our programs create jobs and improve livelihoods, helping families thrive in rural Cambodia.`,
    contents: [
      {
        title: "Rural Development",
        content: `One of our primary efforts is ensuring access to clean and safe water. We help communities construct clean water wells, install water filtration systems, and build sanitation facilities. These projects not only reduce the incidence of waterborne diseases but also free up time—especially for women and girls—who would otherwise spend hours collecting water from distant or unsafe sources.
    We also invest in sustainable agriculture training, providing families with tools, seeds, and techniques that increase crop yields while preserving the environment. By promoting organic farming, composting, and water-efficient irrigation, we empower farmers to secure reliable food sources and improve household income.
    In addition to agriculture, we facilitate livelihood development opportunities through vocational training, small business support, and access to microfinance. These programs help rural families diversify their incomes, reduce poverty, and build financial resilience.
    By working directly with community leaders, we ensure our development initiatives are locally driven, culturally respectful, and sustainable. Our goal is to create thriving rural communities where families have the resources and skills to flourish—now and for generations to come.`,
      },
    ],
  },
];

// Get the ID from the route, convert to number
const programId = parseInt(route.params.id);
const program = ref(programs.find((p) => p.id === programId));
</script>
