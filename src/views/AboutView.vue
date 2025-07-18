
<template>
  <div class="min-h-screen bg-white">
    <section
      class="relative w-full h-[42rem] bg-gradient-to-br from-blue-100 via-purple-100 to-indigo-700"
    >
      <!-- slideshow images -->
      <div class="absolute inset-0 z-0">
        <div
          v-for="(image, index) in images"
          :key="index"
          :class="[
            'absolute inset-0 transition-opacity duration-700 ease-in-out',
            current === index ? 'opacity-100' : 'opacity-0',
          ]"
        >
          <img
            :src="image"
            :alt="`Slide ${index + 1}`"
            class="w-full h-full object-cover object-center"
          />

          <div class="absolute inset-0 bg-black/50"></div>
        </div>
      </div>

      <!-- centered hero card -->
      <div class="absolute inset-0 flex items-center justify-center px-4 z-20">
        <div class="p-10 max-w-2xl text-center">
          <h1
            class="text-4xl sm:text-5xl lg:text-6xl font-bold text-gray-100 mb-6"
          >
            See Our About
          </h1>
          <p class="text-xl text-gray-100 mb-8 leading-relaxed">
            Learn about our solutions in education, training, and care that
            empower vulnerable communities worldwide.
          </p>
          <a
            href="#programs"
            class="bg-pink-600 hover:bg-pink-700 text-white px-8 py-3 text-lg rounded-lg inline-block transition-colors duration-200"
          >
            LEARN MORE
          </a>
        </div>
      </div>

      <!-- dots pagination -->
      <div
        class="absolute z-20 bottom-8 left-1/2 transform -translate-x-1/2 flex space-x-2"
      >
        <button
          v-for="(image, index) in images"
          :key="index"
          @click="goToSlide(index)"
          :aria-label="`Go to slide ${index + 1}`"
          :class="[
            'rounded-full transition-all',
            current === index ? 'bg-white' : 'bg-gray-400',
          ]"
          class="w-2 h-2"
        ></button>
      </div>
    </section>

  <section class="relative py-16 sm:py-24 px-4 sm:px-6 lg:px-8 bg-white">
  <div class="relative max-w-6xl mx-auto flex flex-col md:flex-row items-center md:items-start gap-10">

    <div class="relative flex-shrink-0 group">
      <div class="relative w-72 sm:w-80 md:w-96 lg:w-[450px] h-72 sm:h-80 md:h-96 lg:h-[450px] rounded-full border-[8px] md:border-[12px] border-blue-500 overflow-hidden mx-auto shadow-2xl group-hover:scale-105 transition-transform duration-300 ease-in-out bg-gradient-to-br from-blue-100 to-blue-300">
        <img
          src="https://lotusoutreach.org/wp-content/uploads/2020/02/IMG_9475.jpg"
          alt="Lotus Outreach profile image"
          class="w-full h-full object-cover opacity-95"
        />
        <div class="absolute inset-0 rounded-full border-4 border-white opacity-30"></div>
      </div>

      <div class="absolute -top-4 -left-4 bg-blue-600 text-white p-3 md:p-4 rounded-lg shadow-lg text-center">
        <p class="text-xl md:text-2xl font-bold">23</p>
        <p class="text-sm md:text-base">Years of</p>
        <p class="text-sm md:text-base">Experience</p>
      </div>

      <div class="absolute -bottom-10 -left-4 bg-blue-700 text-white p-3 md:p-4 rounded-lg shadow-lg w-72 md:w-80 text-sm md:text-base">
        <p class="font-semibold mb-1">Together with our partners,</p>
        <p>
          we continue to provide education scholarships, skills training,
          counseling, and safe environments for vulnerable communities
          across Cambodia.
        </p>
      </div>
    </div>

    <div class="flex-1 text-center md:text-left">
      <h1 class="text-3xl sm:text-4xl font-bold text-gray-800 mb-4">History</h1>
      <h2 class="text-xl sm:text-2xl font-semibold text-gray-600 mb-6">
        | Donate For Girls Around The World!
      </h2>
      <p class="text-gray-700 mb-4">
        Lotus Outreach’s work in Cambodia began with a powerful moment when
        founder Khyentse Norbu met a young, partially blind girl at a safe
        house. Touched by her strength, he pledged to support her
        education—an experience that reshaped our mission.
      </p>
      <p class="text-gray-700 mb-4">
        Originally founded in 1993 in India to support refugees, LO expanded
        globally, establishing its U.S. headquarters in 2002.
      </p>
      <p class="text-gray-700">
        <strong class="text-blue-600">Best Addition:</strong> Today, Lotus
        Outreach Cambodia empowers women and girls through education, skills
        training, and community programs—breaking the cycle of poverty and
        creating lasting change.
      </p>
    </div>

  </div>
</section>


    <section class="py-20" id="mission-vision-values">
      <div
        class="max-w-7xl mx-auto px-6 grid md:grid-cols-2 gap-10 items-center"
      >
        <div>
          <h2 class="text-4xl font-bold text-blue-700 mb-8">
            Our Mission, Vision & Values
          </h2>

          <div class="mb-6">
            <div class="flex items-center mb-2">
              <Target class="text-blue-600 w-7 h-7 mr-2" />
              <h3 class="text-xl font-semibold text-blue-800">Our Mission</h3>
            </div>
            <p class="text-gray-700 leading-relaxed">
              To empower vulnerable women and children in Cambodia through
              education, training, and care—helping them break the cycle of
              poverty and live with dignity, opportunity, and hope.
            </p>
          </div>

          <div class="mb-6">
            <div class="flex items-center mb-2">
              <Eye class="text-blue-600 w-7 h-7 mr-2" />
              <h3 class="text-xl font-semibold text-blue-800">Our Vision</h3>
            </div>
            <p class="text-gray-700 leading-relaxed">
              A world where every girl and child, no matter their background,
              has access to quality education, protection, and the tools to
              shape their own future.
            </p>
          </div>

          <div>
            <div class="flex items-center mb-2">
              <Gem class="text-blue-600 w-7 h-7 mr-2" />
              <h3 class="text-xl font-semibold text-blue-800">Our Values</h3>
            </div>
            <p class="text-gray-700 leading-relaxed">
              We believe in dignity, equity, and opportunity for all. With
              compassion, integrity, and resilience, we uplift the vulnerable
              and build brighter futures—one life at a time.
            </p>
          </div>
        </div>

        <div>
          <img
            src="https://lotusoutreach.org/wp-content/uploads/2020/02/IMG_9585-2.jpg"
            alt="Girls with bicycles supported by Lotus Outreach"
            class="rounded-2xl shadow-2xl w-full object-cover"
          />
        </div>
      </div>
    </section>

    <section id="team">
      <div class="container mx-auto px-4 py-12">
        <h2
          class="text-4xl text-blue-700 md:text-6xl font-extrabold text-center mb-16 glow-effect"
          data-aos="fade-up"
        >
          Our Inspired Team
        </h2>

        <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-8">
          <div
            v-for="(member, index) in teamMembers"
            :key="member.name"
            class="text-center transition-all duration-500 hover:-translate-y-2"
            data-aos="zoom-in"
            :data-aos-delay="100 * (index + 1)"
          >
            <div
              class="relative w-48 h-48 mx-auto overflow-hidden rounded-full border-4 border-blue-500"
            >
              <img
                :src="member.image"
                :alt="`Portrait of ${member.name}, ${member.position}`"
                class="w-full h-full object-cover rounded-full transition-transform duration-300 hover:scale-110"
              />
              <div
                class="absolute inset-0 rounded-full bg-indigo-500 opacity-0 hover:opacity-20 transition-opacity duration-300"
              ></div>
            </div>
            <p class="mt-8 text-2xl font-bold text-blue-500">
              {{ member.name }}
            </p>
            <p class="text-black-500 text-lg">{{ member.position }}</p>
          </div>
        </div>
      </div>
    </section>

    <section class="bg-white py-16" id="partners">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 relative">
        <h2
          class="text-3xl sm:text-4xl font-bold text-blue-700 mb-10 flex items-center"
        >
          Our Value Partners
        </h2>

        <div class="relative overflow-hidden">
          <div
            class="flex whitespace-nowrap animate-marquee"
            :style="{
              '--marquee-width': marqueeWidth,
              '--marquee-duration': marqueeDuration + 's',
            }"
            @mouseenter="pauseMarquee"
            @mouseleave="resumeMarquee"
          >
            <div
              v-for="(partner, index) in partnerLogos"
              :key="index"
              class="inline-flex flex-col items-center justify-center bg-gray-50 rounded-xl shadow hover:shadow-md transition duration-300 cursor-pointer mr-6 flex-shrink-0"
              style="min-width: 160px; height: 128px"
            >
              <a
                :href="partner.url"
                target="_blank"
                rel="noopener noreferrer"
                class="flex items-center justify-center w-full h-full"
                :title="partner.info"
              >
                <img
                  :src="partner.img"
                  :alt="`Logo of ${partner.info}`"
                  class="max-h-20 object-contain px-4"
                />
              </a>
              <p class="mt-2 text-center text-sm text-gray-600">
                {{ partner.info }}
              </p>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount, nextTick } from "vue";
import AOS from "aos";
import "aos/dist/aos.css";
import { Target, Eye, Gem, ChevronLeft, ChevronRight } from "lucide-vue-next";

// Define types for TypeScript (optional, remove if not using TypeScript)
interface TeamMember {
  name: string;
  position: string;
  image: string;
}

interface Partner {
  img: string;
  url: string;
  info: string;
}

const images = ref<string[]>([
  "https://lotusoutreach.org/wp-content/uploads/2019/08/header.jpg",
  "https://lotusoutreach.org/wp-content/uploads/2020/02/IMG_9585-2.jpg",
  "https://helpcode.ch/wp-content/uploads/2017/07/CCS-4-750x498.jpg",
]);

const current = ref<number>(0);

const nextSlide = () => {
  current.value = (current.value + 1) % images.value.length;
};

const prevSlide = () => {
  current.value =
    (current.value - 1 + images.value.length) % images.value.length;
};

const goToSlide = (index: number) => {
  current.value = index;
};

let interval: ReturnType<typeof setInterval> | null = null;
onMounted(() => {
  interval = setInterval(nextSlide, 5000);
  AOS.init({ duration: 1000, once: true });
});
onBeforeUnmount(() => {
  if (interval) clearInterval(interval);
});

const teamMembers = ref<TeamMember[]>([
  {
    name: "Glenn Fawcett",
    position: "Executive Director",
    image:
      "https://lotusoutreach.org/wp-content/uploads/2020/02/IMG_9668-1024x768.jpg",
  },
  {
    name: " Raksmey Var",
    position: "Country Representative, Cambodia",
    image:
      "https://lotusoutreachaustralia.org.au/wp-content/uploads/2015/07/Raksmey-for-web-site-.jpg",
  },
  {
    name: "Pisey Chea",
    position: "LOCAM Project Officer",
    image:
      "https://lotusoutreachaustralia.org.au/wp-content/uploads/2018/06/Untitled-design-2.jpg",
  },
  {
    name: "Borika",
    position: "Accountant, Cambodia",
    image: "https://lotusoutreach.org/wp-content/uploads/2022/08/borika.jpeg",
  },
]);

const originalPartnerLogos = [
  {
    img: "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRo_2n4ixhk90E0WEDNpghs_skGLtJZuMNCGfqyiBtnwoKRjd8DRZxCgLlmGYCwm9fuGAg&usqp=CAU",
    url: "https://www.passerellesnumeriques.org/what-we-do/cambodia/",
    info: "Passerelles Numériques",
  },
  {
    img: "http://cwcc.org.kh/wp-content/uploads/2024/07/cropped-logo-4.png",
    url: "http://cwcc.org.kh/",
    info: "CWCC",
  },
  {
    img: "https://bettercarenetwork.org/sites/default/files/styles/max_325x325/public/2022-07/cocd_cambodia_logo.jpeg?itok=M_TusQPl",
    url: "https://cocd-cambodia.org/",
    info: "COCD Cambodia",
  },
  {
    img: "https://kapekh.org/files/Logos/004_Small.png",
    url: "https://www.kapekh.org/",
    info: "KAPE Cambodia",
  },
  {
    img: "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQG-PHDrMqX-Qnh5xX45XjwvCk6Z_96G_Y2bw&s",
    url: "https://www.khemaracambodia.org/",
    info: "Khemara Cambodia",
  },
  {
    img: "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQkp_i6a7QoF16LhEl4pyBL1-TVeMvnXSjHpA&s",
    url: "https://www.ccc-cambodia.org/en/ngodb/ngo-information/914",
    info: "CCC Cambodia",
  },
  {
    img: 'https://i.imgur.com/3RCrIcD.png',
    url: 'https://www.whitelotustrust.org/',
    info: 'White Lotus Trust',
  },
  {
    img: "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRtqDNr8W1xVsYI1MO7mo-uIZjb6bQKKUHNJA&s",
    url: "https://www.thegardenofpeace.org/",
    info: "Garden of Peace",
  },
  {
    img: "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTD0I4XK5CYJ88Qxs0rid0x8xBd9yu8cesDag&s",
    url: "https://www.primerospasos.org/",
    info: "Primero Pasos",
  },
  {
    img: "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQHRdeUeM-UWygfL6JSu5qFNImCJ6n8B2MBAQ&s",
    url: "https://mulheresdaparada.org/",
    info: "Mulheres da Parada",
  },
];

// Duplicate the logos multiple times to ensure a continuous loop for CSS animation
// We'll duplicate it 4 times to ensure seamless scrolling even on wider screens
const partnerLogos = ref<Partner[]>([
  ...originalPartnerLogos,
  ...originalPartnerLogos,
  ...originalPartnerLogos,
  ...originalPartnerLogos,
]);

const marqueeWidth = ref("0px");
const marqueeDuration = ref(30); // Adjust this value (in seconds) for desired speed. Lower = faster.

const calculateMarqueeWidth = () => {
  if (originalPartnerLogos.length === 0) {
    marqueeWidth.value = "0px";
    return;
  }
  // Assuming each logo item is 160px wide (min-width) + 24px (mr-6)
  const singleLogoItemWidth = 160 + 24;
  marqueeWidth.value = `${originalPartnerLogos.length * singleLogoItemWidth}px`;

  // You can dynamically adjust duration based on number of logos
  // For example, 2 seconds per logo for a consistent 'speed' feeling
  // marqueeDuration.value = originalPartnerLogos.length * 2;
};

// Controls for pausing/resuming CSS animation on hover
const pauseMarquee = (event: Event) => {
  if (event.currentTarget instanceof HTMLElement) {
    event.currentTarget.style.animationPlayState = "paused";
  }
};

const resumeMarquee = (event: Event) => {
  if (event.currentTarget instanceof HTMLElement) {
    event.currentTarget.style.animationPlayState = "running";
  }
};

onMounted(() => {
  // Ensure DOM is ready before calculating width for the marquee
  nextTick(() => {
    calculateMarqueeWidth();
  });
  interval = setInterval(nextSlide, 5000);
  AOS.init({ duration: 1000, once: true });
});

onBeforeUnmount(() => {
  if (interval) clearInterval(interval);
});
</script>


<style>
/* Define the keyframes for the marquee animation */
@keyframes marquee {
  0% {
    transform: translateX(0);
  }
  100% {
    transform: translateX(calc(-1 * var(--marquee-width)));
  }
}

/* Apply the animation to the container */
.animate-marquee {
  animation: marquee var(--marquee-duration, 60s) linear infinite;
}
</style>