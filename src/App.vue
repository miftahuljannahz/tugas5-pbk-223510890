<template>
  <q-layout view="hHh lpR fFf">
    <q-header elevated class="bg-pink-9 text-white">
      <q-toolbar class="bg-soft-pink">
        <q-btn flat round dense icon="menu" @click="leftDrawerOpen = !leftDrawerOpen" />
        <q-toolbar-title>
          <q-avatar class="profile">
            <img src="https://i.pinimg.com/564x/53/99/53/5399532498fc012986423d5b14a36b24.jpg" alt="Logo" size="45px"/>
          </q-avatar>
          Mita's Bakery
        </q-toolbar-title>
        <q-space />
        <q-input
          filled
          dense
          placeholder="Cari produk..."
          prepend-icon="search"
          class="bg-white q-ma-none"
        >
          <template v-slot:append>
            <q-icon name="shopping_cart" />
          </template>
        </q-input>
      </q-toolbar>
    </q-header>

    <q-drawer v-model="leftDrawerOpen" side="left" class="bg-soft-pink" :overlay="false">
      <q-list>
        <q-item clickable v-ripple>
          <q-item-section>
            <q-btn flat style="color:black" label="Menu" />
          </q-item-section>
        </q-item>
        <q-item clickable v-ripple>
          <q-item-section>
            <q-btn flat style="color:black;" label="Promo" />
          </q-item-section>
        </q-item>
        <q-item clickable v-ripple>
          <q-item-section>
            <q-btn flat style="color:black;" label="Store" />
          </q-item-section>
        </q-item>
        <q-item clickable v-ripple>
          <q-item-section>
            <q-btn style="background: #ff69b4; color: white" label="Login" />
          </q-item-section>
        </q-item>
      </q-list>
    </q-drawer>

    <q-page-container>
      <div class="q-pa-md">
        <div class="q-gutter-md">
          <q-carousel
            v-model="slide"
            transition-prev="slide-right"
            transition-next="slide-right"
            swipeable
            animated
            control-color="white"
            navigation
            padding
            arrows
            height="650px"
            class="bg-pink text-white shadow-1 rounded-borders"
          >
            <q-carousel-slide
              v-for="(item, index) in slides"
              :key="index"
              :name="'slide' + index"
              class="column no-wrap flex-center"
            >
              <q-img
                :src="item.image"
                :alt="'Slide ' + (index + 1)"
                style="width: 100%; height: 100%; object-fit: cover !important"
              />
              <div class="q-mt-md text-center">
                {{ item.text }}
              </div>
            </q-carousel-slide>
          </q-carousel>
        </div>
      </div>

      <div class="q-pa-md row items-start q-gutter-md">
        <q-card
          v-for="(product, index) in products"
          :key="index"
          class="my-card"
          flat
          bordered
        >
          <q-img :src="product.image" class="same-size-image" />
          <q-card-section>
            <div class="text-h5 q-mt-sm q-mb-xs">{{ product.title }}</div>
            <div class="text-caption text-grey">{{ product.description }}</div>
          </q-card-section>
          <q-card-actions>
            <q-btn flat color="pink-10" label="Share" style="font-weight: 550;" />
            <q-btn flat color="pink-8" label="Keranjang" style="font-weight: 550;" />
            <q-space />
            <q-btn
              color="grey"
              round
              flat
              dense
              :icon="expandedIndex === index ? 'keyboard_arrow_up' : 'keyboard_arrow_down'"
              @click="toggleExpand(index)"
            />
          </q-card-actions>
          <q-slide-transition>
            <div v-show="expandedIndex === index">
              <q-separator />
              <q-card-section class="text-subtitle2">
                {{ product.moreInfo }}
              </q-card-section>
            </div>
          </q-slide-transition>
        </q-card>
      </div>
    </q-page-container>

    <footer class="footer bg-pink-9 text-white">
      <p>Miftahul Jannah | 223510890</p>
    </footer>
  </q-layout>
</template>

<script>
import { ref, onMounted } from "vue";

export default {
  setup() {
    const slide = ref(0);
    const leftDrawerOpen = ref(false);
    const slides = ref([
      {
        image:
          "https://fazz.com/id/wp-content/uploads/sites/3/2024/01/pastry-1.jpg",
      },
      {
        image:
          "https://m.media-amazon.com/images/S/assets.wholefoodsmarket.com//content/df/98/6168c1c449489ffa778a198d6a9a/bakery-hero1500x600-2x-v2._TTW_._CR0,0,3000,1200_._SR2000,800_._QL100_.jpg",
      },
      {
        image:
          "https://www.posist.com/restaurant-times/wp-content/uploads/2016/10/A-Detailed-Guide-On-Starting-A-Bakery-Business-In-India-In-2023.jpg",
      },
      {
        image:
          "https://img.freepik.com/free-vector/doodles-background-bakery_125540-632.jpg",
        text: "Story",
      },
    ]);

    const lorem =
      "Kami di Mita's Bakery percaya bahwa setiap momen istimewa layak dihiasi dengan manisnya kue dan kelezatan roti. Mari bersama-sama buat momen-momen berharga dengan rasa dari hati.";

    onMounted(() => {
      setTimeout(() => {
        slide.value = 0;
      }, 100);
    });

    const expandedIndex = ref(null);
    const products = ref([
      {
        image: 'https://soesmerdeka.com/wp-content/uploads/2021/07/Untitled-1Artboard-2-2.png',
        title: 'Brownies Almond',
        description: 'Rp 83.000',
        moreInfo: 'Legitnya brownies panggang coklat yang renyah dibagian luar dan lembut dibagian dalam dengan kacang almond panggang premium, sangat cocok menjadi sajian nikmat di sore hari.'
      },
      {
        image: 'https://www.static-src.com/wcsstore/Indraprastha/images/catalog/full//96/MTA-91623407/clairmont-cake_tiramisu-cake_full01.jpg',
        title: 'Kue Tiramisu 15 X 15 Cm',
        description: 'Rp 149.000',
        moreInfo: 'Spons vanilla lembut dilapisi dengan puding tiramisu.'
      },
      {
        image: 'https://www.static-src.com/wcsstore/Indraprastha/images/catalog/full//102/MTA-91072928/no_brand_lapis_legit_keju_premium_asli_surabaya_moist_dengan_resep_kuno_18x6_cm_full02_ibfs0mxj.jpg',
        title: 'Lapis Legit Keju',
        description: 'Rp 705.000',
        moreInfo: 'Sajikan kue lapis legit keju di hari spesial anda atau sebagai hadiah untuk kerabat, rekan dan teman anda. Terbuat dari bahan-bahan berkualitas dan resep khas Holland Bakery. Dikemas dengan plastik bersegel sehingga terjamin higenis dan produk lebih tahan lama meskipun di suhu ruangan'
      },
      {
        image: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSdghRtnEEvVSpuPyiJoHyf-DAnZ-mh4KR8htreUnwrpQ&s',
        title: 'Kue Dadar Gulung 15 Cm',
        description: 'Rp 143.000',
        moreInfo: 'Cake modern Mita Bakery dengan citra rasa tradisional gula kelapa nan gurih '
      },
    ]);

    const toggleExpand = (index) => {
      expandedIndex.value = expandedIndex.value === index ? null : index;
    };

    return {
      slide,
      slides,
      lorem,
      products,
      expandedIndex,
      toggleExpand,
      leftDrawerOpen,
    };
  },
};
</script>

<style scoped>
.q-carousel {
  margin-bottom: 0; /* Menghilangkan margin bawah pada carousel */
}

.my-card {
  margin-bottom: 0; /* Menghilangkan margin bawah pada card */
}

.footer {
  background-color: #333;
  color: #fff;
  padding: 20px 0;
  text-align: center;
}
.flex-between {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: #ffe4e1;
  padding: 1rem 3rem;
}

.left {
  display: flex;
  align-items: center;
}

.right {
  display: flex;
  align-items: center;
}

.profile {
  border-radius: 50%;
  overflow: hidden;
}

.same-size-image {
  width: 100%;
  height: 200px;
  object-fit: cover;
}

.q-carousel-slide {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.rounded-borders {
  border-radius: 15px;
}

.q-gutter-md > .q-card {
  margin-bottom: 20px;
}

.bg-pink {
  background-color: #ffc0cb !important;
}

.bg-pink-9 {
  background-color:  #ffc0cb !important;
}

.bg-soft-pink {
  background-color: #ffc0cb !important;
}
</style>
