
<template>
  <div class="container mx-auto">
    <section class="m-4 md:m-8">
      <div class="flex flex-col lg:flex-row lg:items-stretch">
        <div class="w-full mb-6 lg:w-1/2 lg:mr-6 lg:mb-0">
          <div class="relative rounded-lg overflow-hidden shadow-md" :style="{paddingTop: `${400 * 100/ 713}%`}">
            <ImageCarousel
              class="absolute inset-0 w-full h-full"
              :items="banners"
            />
          </div>
        </div>
        <div class="w-full lg:w-1/2">
          <div class="relative" :style="{paddingTop: `${400 * 100/ 713}%`}">
            <div class="absolute inset-0 w-full h-full top-grid">
              <CallCard class="top-grid__call-card" title="Call Center" subtitle="Nomor Darurat" number="119" />
              <CallCard class="top-grid__call-card" title="Dinkes Jabar" subtitle="Pertanyaan Umum" number="0811 2093 306" />
              <div
                v-show="cases"
                class="top-grid__call-status rounded-lg"
              >
                <h6>
                  <strong>Pertanyaan Terlayani</strong><br>
                  <small>
                    Telpon & Pesan Teks
                  </small>
                </h6>
                <summary class="text-5xl text-yellopx-40 font-bold">
                  {{ cases ? cases.pertanyaan_terlayani : '' }}
                </summary>
              </div>
              <div
                v-show="!cases"
                class="top-grid__call-status rounded-lg"
              >
                <ContentLoader
                  :speed="2"
                  :height="100"
                  primary-color="rgba(255,255,255,0.3)"
                  secondary-color="rgba(255,255,255,0.1)"
                  class="w-full h-full max-w-xs"
                  style="grid-column-end: span 2;"
                >
                  <rect
                    x="0"
                    y="0"
                    rx="8"
                    ry="6"
                    width="50%"
                    height="16"
                  />
                  <rect
                    x="0"
                    y="30"
                    rx="8"
                    ry="6"
                    width="66%"
                    height="16"
                  />
                  <rect
                    x="0"
                    y="64"
                    rx="8"
                    ry="6"
                    width="20%"
                    height="16"
                  />
                </ContentLoader>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
    <section class="mt-8 m-4 md:m-8 flex flex-col">
      <h2 class=" text-lg md:text-2xl">
        <b>Angka Kejadian di Jawa Barat</b><br>
        <small class="opacity-50">Update Terakhir: {{ lastUpdatedAt }}</small>
      </h2>
      <DataSummary class="my-8" />
      <div class="rounded-lg bg-white shadow-md overflow-hidden">
        <PetaPersebaranAllCases />
      </div>
      <a
        v-show="false"
        target="_blank"
        class="text-center md:self-center w-56 py-2 rounded-lg text-brand-green-darker hover:bg-green-200 border-2 border-solid border-brand-green"
        href="/data"
      >
        Lihat Data Selengkapnya
      </a>
      <br>
    </section>
    <section class="mt-8 m-4 md:mt-16 md:m-8">
      <h2 class="mb-0 md:mb-4 text-left text-2xl md:text-center md:text-3xl">
        <b>Apa yang Harus Dilakukan</b>
      </h2>
      <div class="p-5 mt-4 md:mt-12 md:p-8 rounded-lg bg-brand-green-dark">
        <h3 class="text-xl lg:text-2xl text-white">
          <strong>Ketahui Resiko dari COVID-19</strong>
        </h3>
        <br>
        <div class="flex flex-col lg:flex-row justify-between items-start">
          <p class="text-white text-lg w-full lg:w-2/3">
            COVID-19 merupakan penyakit yang disebabkan Novel Coronavirus 2019.
            Meski bergejala mirip dengan flu biasa, COVID-19 sampai saat ini memiliki fatalitas lebih tinggi.
            Virus ini juga menyebar dengan sangat cepat karena bisa pindah dari orang ke orang bahkan sebelum orang tersebut tidak menunjukkan gejala.
            <br>
            <br>
            Penting bagi Anda untuk menilai kondisi secara mandiri. Anda bergejala?
          </p>
          <i style="flex: 0 0 2rem;" />
          <!-- <button class="px-10 py-2 rounded-lg text-white border-2 border-solid border-white hover:bg-brand-green-light">
            Lihat Disini
          </button> -->
          <a
            class="cursor-pointer px-10 py-4 rounded-lg text-white border-2 border-solid border-white hover:bg-brand-green-light"
            :href.prop="selfDiagnoseURL"
            target="_blank"
          >
            <b>Nilai Diri Saya</b>
          </a>
        </div>
      </div>
      <div class="flex flex-row flex-wrap items-stretch my-8">
        <div
          class="w-full mb-8 lg:mb-0 lg:w-1/4 rounded-lg bg-white shadow-md lg:mr-8 p-5 md:p-8"
          style="min-width:320px"
        >
          <div class="flex flex-col justify-between items-start h-full">
            <header>
              <h3 class="text-lg lg:text-2xl">
                <strong>Punya Pertanyaan Terkait COVID-19?</strong>
              </h3>
              <br>
              <br>
              <p>
                Penting bagi Anda untuk menilai kondisi secara mandiri.
                Anda bergejala?
              </p>
            </header>
            <nuxt-link
              tag="a"
              class="mt-8 px-6 py-4 inline-block rounded-lg bg-brand-green text-white border-2 border-solid border-brand-green"
              to="/faq"
            >
              <b>Tanyakan Sekarang</b>
            </nuxt-link>
          </div>
        </div>
        <div class="flex-1 rounded-lg bg-white shadow-md p-5 md:p-8">
          <div class="flex flex-col items-stretch">
            <h3 class="text-lg lg:text-2xl leading-loose">
              <strong>Hubungi Call Center</strong>
            </h3>
            <CallCenter :count="4" />
            <br>
            <nuxt-link
              tag="a"
              to="/contact"
              class="text-center md:self-center w-64 py-4 rounded-lg text-brand-green-darker hover:bg-green-200 border-2 border-solid border-brand-green"
            >
              Lihat Selengkapnya
            </nuxt-link>
          </div>
        </div>
      </div>
      <div class="flex flex-col items-stretch my-4 p-5 md:p-8 md:p-12 bg-white rounded-lg shadow-md">
        <h3 class="text-lg lg:text-2xl">
          <strong>Daftar Rumah Sakit Rujukan di Jawa Barat</strong>
        </h3>
        <br>
        <p class="opacity-75">
          Berikut ini adalah rumah sakit yang menjadi rujukan untuk pasien dengan status Pasien dalam Pengawasan.
          Anda harus mengunjungi fasilitas kesehatan terdekat terlebih dahulu seperti klinik/rumah sakit umum sebelum akhirnya dapat dirujuk ke rumah sakit khusus di bawah ini.
        </p>
        <br>
        <br>
        <ul class="hospital-list">
          <li
            v-for="(h, index) in hospitals"
            :key="index"
          >
            <ContactListItem v-bind="h" />
          </li>
        </ul>
        <br>
        <nuxt-link
          tag="a"
          to="/contact"
          class="text-center md:self-center px-4 py-2 rounded-lg text-brand-green-darker hover:bg-green-200 border-2 border-solid border-brand-green"
        >
          Lihat Rumah Sakit Lainnya
        </nuxt-link>
      </div>
    </section>
    <section class="mt-8 m-4 md:m-8 rounded-lg bg-white shadow-md p-5 md:p-8">
      <header class="lg:max-w-2xl">
        <h2 class="mb-4 md:mb-8 text-left text-xl md:text-2xl">
          <b>Lindungi Diri dan Orang Lain</b>
        </h2>
        <p>
          Sampai saat ini COVID-19 belum memiliki vaksin, sehingga cara terbaik untuk tidak terinfeksi adalah dengan menghindari terekspos virus.
        </p>
      </header>
      <br>
      <div class="flex flex-col items-stretch lg:max-w-2xl">
        <article class="text-gray-800">
          <h3 class="text-lg text-black">
            <b>COVID-19 dapat menyebar dari orang ke orang melalui tetesan kecil (droplet) saat batuk atau bersin.
              Maka yang bisa Anda lakukan adalah:
            </b>
          </h3>
          <br>
          <ul style="list-style-type: none;">
            <li class="li-check-mark">
              Sering cuci tangan dengan sabun atau hand-sanitizer
            </li>
            <li class="li-check-mark">
              Hindari menyentuh wajah, terutama hidung, mulut, dan mata
            </li>
            <li class="li-check-mark">
              Bersihkan permukaan benda yang disentuh banyak orang
            </li>
            <li class="li-check-mark">
              Social Distancing! Minimalisir kontak fisik dengan sesama
            </li>
            <li class="li-check-mark">
              Jaga jarak 1-3 meter dengan orang yang sakit
            </li>
            <li class="li-check-mark">
              Jika sakit, maka:
              <ol style="list-style-type: decimal; list-style-position: inside;">
                <li class="ml-0">
                  Tinggal di rumah
                </li>
                <li class="ml-0">
                  Gunakan masker
                </li>
              </ol>
            </li>
          </ul>
        </article>
        <nuxt-link
          v-show="false"
          tag="a"
          to="#"
          class="text-center md:self-center px-4 py-2 rounded-lg text-brand-green-darker hover:bg-green-200 border-2 border-solid border-brand-green"
        >
          Lihat Selengkapnya
        </nuxt-link>
      </div>
    </section>
    <section class="mt-2 m-4 md:mt-4 md:m-8 rounded-lg bg-white shadow-md p-5 md:p-8">
      <h2 class="mb-4 md:mb-8 text-left text-xl md:text-2xl">
        <b>Kenapa harus Social Distancing (Jaga Jarak Sesama)?</b>
      </h2>
      <article class="flex flex-col lg:flex-row">
        <img
          v-lazy="'https://firebasestorage.googleapis.com/v0/b/jabarprov-covid19.appspot.com/o/public%2Fflatten.png?alt=media&token=afe8bb16-6cd5-4056-8d14-5c102f34a7c9'"
          class="order-2 lg:order-1 w-full h-full mb-8 lg:w-1/2 lg:mr-8 object-contain md:object-cover object-center rounded-lg"
        >
        <div class="order-1 lg:order-2 lg:w-1/2">
          <p class="mb-4">
            COVID-19 menyebar dengan cepat.
            Orang dapat terinfeksi tanpa menunjukkan gejala, namun tetap dapat menyebarkannya ke orang lain.
            Jika kita tidak melakukan upaya pencegahan berupa menghindari keramaian,
            jumlah orang terinfeksi akan meledak dan fasilitas layanan kesehatan akan kewalahan sehingga banyak kasus akan tidak tertangani.
          </p>
          <p class="font-bold text-lg">
            Social distancing akan mengurangi laju penularan dan mengizinkan pasien terinfeksi untuk ditangani hingga sembuh, seperti di grafik terlampir.
          </p>
        </div>
      </article>
    </section>
    <section class="mt-8 m-4 md:mt-16 md:m-8">
      <h2 class="mb-4 md:mb-8 text-left text-2xl md:text-center md:text-3xl">
        <b>Apa yang Harus Diketahui</b>
      </h2>
      <div class="flex flex-col items-stretch">
        <article class="html-content text-gray-800 flex flex-col lg:flex-row">
          <img v-lazy="'https://firebasestorage.googleapis.com/v0/b/jabarprov-covid19.appspot.com/o/public%2Fcovid-19.jpg?alt=media&token=3dbbb851-546b-4154-be27-ed8692f194a5'" class="hidden lg:block w-full h-full lg:w-1/2 lg:mr-8 object-cover object-center rounded-lg">
          <div class="w-full lg:w-1/2">
            <h3 class="text-xl text-black">
              <b>Apa Itu COVID-19?</b>
            </h3>
            <p>
              COVID-19 adalah penyakit yang disebabkan oleh Novel Coronavirus (2019-nCoV),
              jenis baru coronavirus yang pada manusia menyebabkan penyakit mulai flu biasa
              hingga penyakit yang serius seperti Middle East Respiratory Syndrome (MERS)
              dan Sindrom Pernapasan Akut Berat/ Severe Acute Respiratory Syndrome (SARS).
            </p>
            <p>
              Pada 11 Februari 2020, World Health Organization (WHO) mengumumkan nama penyakit yang disebabkan 2019-nCov,
              yaitu <strong>Coronavirus Disease (COVID-19).</strong>
            </p>
            <h3 class="text-xl text-black">
              <b>Gejala</b>
            </h3>
            <p>
              Gejala umum berupa demam ≥38°C, batuk kering, dan sesak napas.
              Jika ada orang yang dalam 14 hari sebelum muncul gejala tersebut pernah melakukan perjalanan ke negara terjangkit,
              atau pernah merawat/kontak erat dengan penderita COVID-19,
              maka terhadap orang tersebut akan dilakukan pemeriksaan laboratorium lebih lanjut untuk memastikan diagnosisnya.
            </p>
            <h3 class="text-xl text-black">
              <b>Penularan</b>
            </h3>
            <p>
              Seseorang dapat terinfeksi dari penderita COVID-19.
              Penyakit ini dapat menyebar melalui tetesan kecil (droplet) dari hidung atau mulut pada saat batuk atau bersin.
              Droplet tersebut kemudian jatuh pada benda di sekitarnya.
              Kemudian jika ada orang lain menyentuh benda yang sudah terkontaminasi dengan droplet tersebut,
              lalu orang itu menyentuh mata, hidung atau mulut (segitiga wajah), maka orang itu dapat terinfeksi COVID-19.
              Seseorang juga bisa terinfeksi COVID-19 ketika tanpa sengaja menghirup droplet dari penderita.
              Inilah sebabnya mengapa kita penting untuk menjaga jarak hingga kurang lebih satu meter dari orang yang sakit.
            </p>
          </div>
        </article>
        <nuxt-link
          v-show="false"
          tag="a"
          to="#"
          class="text-center md:self-center px-4 py-2 rounded-lg text-brand-green-darker hover:bg-green-200 border-2 border-solid border-brand-green"
        >
          Lihat Selengkapnya
        </nuxt-link>
      </div>
    </section>
    <section class="mt-8 m-4 md:mt-16 md:m-8">
      <div class="flex justify-between items-center md:mb-4">
        <h2 class="text-left text-2xl md:text-3xl">
          <b>Info Praktikal</b>
        </h2>
        <nuxt-link
          tag="a"
          class="hidden md:inline-block text-center md:self-center px-4 py-2 rounded-lg text-brand-green-darker hover:bg-green-200 border-2 border-solid border-brand-green"
          to="/infographics"
        >
          Lihat Selengkapnya
        </nuxt-link>
      </div>
      <ShareableItems :items="shareableInfographics" />
      <nuxt-link
        tag="a"
        class="inline-block md:hidden text-center md:self-center px-4 py-2 mt-8  rounded-lg text-brand-green-darker hover:bg-green-200 border-2 border-solid border-brand-green"
        to="/infographics"
      >
        Lihat Selengkapnya
      </nuxt-link>
    </section>
    <br>
    <section class="m-4 md:m-8">
      <div class="flex flex-col items-stretch p-8 rounded-lg bg-white shadow-md">
        <h2 class="text-left text-2xl md:text-3xl">
          <b>Berita Jabar</b>
        </h2>
        <br>
        <br>
        <div>
          <div
            v-for="(item, index) in news"
            :key="index"
          >
            <BlogPostPreview
              :image="item.image"
              :title="item.title"
              :content="item.content"
              :date="formatDateTimeShort(item.published_at)"
              :to="item.route"
            />
            <hr v-if="index < news.length - 1" class="my-8">
          </div>
        </div>
        <br>
        <nuxt-link
          tag="a"
          class="text-center md:self-center px-4 py-2 mt-8 rounded-lg text-brand-green-darker hover:bg-green-200 border-2 border-solid border-brand-green"
          to="/articles?tab=jabar"
        >
          Lihat Selengkapnya
        </nuxt-link>
      </div>
    </section>
  </div>
</template>
<script>
import { ContentLoader } from 'vue-content-loader'
import { mapState } from 'vuex'
import { faChevronRight } from '@fortawesome/free-solid-svg-icons'
import { formatDateTimeShort } from '~/lib/date'
import ImageCarousel from '~/components/ImageCarousel'
import CallCard from '~/components/CallCard'
import ContactListItem from '~/components/ContactList/ContactListItem'
import CallCenter from '~/components/CallCenter'
import BlogPostPreview from '~/components/Blog/BlogPostPreview'
import DataSummary from '~/components/_pages/index/DataSummary'
import PetaPersebaranAllCases from '~/components/Tableau/PetaPersebaranAllCases'
import ShareableItems from '~/components/ShareableItems'

export default {
  components: {
    ContentLoader,
    ImageCarousel,
    CallCard,
    BlogPostPreview,
    ContactListItem,
    CallCenter,
    DataSummary,
    PetaPersebaranAllCases,
    ShareableItems
  },
  data () {
    return {
      icon: {
        faChevronRight
      },
      todayDateAndTime: formatDateTimeShort(new Date())
    }
  },
  computed: {
    ...mapState({
      banners: state => state.banners.items,
      hospitals: state => state.hospitals.items.filter((_, index) => index < 3),
      remainingHospitalCount: state => state.hospitals.items.length - 3,
      infographics: state => state.infographics.items,
      news: state => state.news.items,
      cases: state => state.statistics.cases
    }),
    selfDiagnoseURL () {
      const config = this.$store.state['remote-config'].config
      return config ? config.selfDiagnoseURL : null
    },
    bannerImage () {
      if (this.banners && this.banners.length) {
        return this.banners[0].url
      }
      return null
    },
    lastUpdatedAt () {
      if (!this.cases) {
        return ''
      }
      return this.formatDateTimeShort(this.cases.updated_at)
    },
    countOf () {
      if (!this.cases) {
        return {}
      }
      const { odp, pdp, aktif } = this.cases
      return {
        odp: odp.total.jabar,
        pdp: pdp.total.jabar,
        aktif: aktif.jabar
      }
    },
    shareableInfographics () {
      return this.infographics
        .filter((_, index) => index < 4)
        .map((item) => {
          return {
            title: item.title,
            route: item.route,
            shareable: true,
            downloadable: true,
            downloadURL: item.images[0],
            shareText: `[Pikobar] Bagikan "${item.title}". Selengkapnya di ${window.location.origin}${item.route}`
          }
        })
    }
  },
  methods: {
    formatDateTimeShort
  }
}

</script>

<style lang="scss" scoped>
.top-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: auto 1fr;
  column-gap: 1.5rem;
  row-gap: 1.5rem;

  &__banner {
    position: relative;
    width: 100%;
    height: 100%;
    padding-top: 58.625%;
    grid-column-end: span 2;
    grid-row-end: span 2;
    border-radius: 0.5rem;
    @apply shadow-md;
  }

  &__call-card {
    min-height: 100px;
    grid-column-end: span 1;
    @apply shadow-md;
  }

  &__call-status {
    grid-column: span 2;
    @apply p-5 flex items-center justify-between
    text-xl text-white
    bg-brand-green-dark
    shadow-md;
  }
}

.hospital-list {
  display: block;
  @screen lg {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    align-items: stretch;
  }
}

.li-check-mark {
  margin-left: 0;
  padding: 0 0 0.5rem 2.5rem;
  background-image: url('/img/check-mark.png');
  background-position: left top;
  background-size: 1.5rem 1.5rem;
  background-repeat: no-repeat;
}

.responded-question {
  grid-column: auto / span 2;

  @screen lg {
    grid-column: auto;
  }
}
.call-cards {
  display: grid;
  grid-template-columns: 1fr 1fr;
  column-gap: 1rem;
  row-gap: 1rem;

  @screen lg {
    grid-template-columns: 1fr 1fr 1fr;
  }
}
.counter-cards {

  @screen lg {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    column-gap: 1.5rem;
    align-items: stretch;
    row-gap: 1.5rem;
  }
}
</style>
