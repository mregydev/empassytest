<template>
  <div class="container">
    <header>
      <VImg class="header-img" src="https://www.godigit.com/content/dam/godigit/directportal/en/egypt-emblem.jpg"
        height="50" />
      <div class="header-title"> {{ $t('title') }}</div>

      <div class="header-translate">
        <VImg class="translate-img" @click="changeLanguage('de')"
          src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQBA2MjoH6BDah2SAQg_idWv9XLBhcK1qZa1w&s" />
        <VImg class="translate-img" @click="changeLanguage('en')"
          src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQN6NjUzMsxiPYELyWrKg17MA4eLo47fkkM2w&s" />
      </div>
    </header>

    <div class="main-content">
      <nav>
        <div class="list">
          <div @click="showHome()" class="list-item">
            {{ $t('homePage') }}
          </div>
          <div @click="showAmbassador()" class="list-item">
            {{ $t('ambassador') }}
          </div>
          <div @click="showEmpassy()" class="list-item">
            {{ $t("embassy") }}
          </div>
        </div>
      </nav>
      <div v-if="isHomePage" class="viewer">
        <VCarousel cycle interval="5000" hide-delimiters height="200">
          <VCarouselItem
            src="https://www.freewebheaders.com/wp-content/gallery/great-pyramid-of-giza/the-great-pyramid-of-giza-egypt-website-header.jpg">
          </VCarouselItem>
          <VCarouselItem
            src="https://www.freewebheaders.com/wp-content/gallery/great-pyramid-of-giza/cache/pyramids-of-giza-egypt-website-header.jpg-nggid043062-ngg0dyn-1280x375x100-00f0w010c010r110f110r010t010.jpg">
          </VCarouselItem>
        </VCarousel>
        <VAlert class="alert" type="warning" closable>
          {{ $t('notification') }}
        </VAlert>

        <h3>{{ $t('mainTitle') }}</h3>
        <div class="description">{{ $t('egyptDescription') }}</div>

      </div>

      <div v-if="isAmbassador">
        <h3>{{ $t('ambassadorPage') }}</h3>
      </div>

      <div v-if="isEmbassy">
        <h3>{{ $t('embassyPage') }}</h3>
      </div>
    </div>
  </div>
</template>

<script setup>

const isHomePage = ref(true)
const isAmbassador = ref(false)
const isEmbassy = ref(false)
onMounted(() => {
  const lang = useRoute().query.lang
  debugger;
  if (lang) {
    i18n.locale.value = lang
  }
})

const showHome = () => {
  isHomePage.value = true;
  isAmbassador.value = false;
  isEmbassy.value = false;
}

const showAmbassador = () => {
  isHomePage.value = false;
  isAmbassador.value = true;
  isEmbassy.value = false;
}

const showEmpassy = () => {
  isHomePage.value = false;
  isAmbassador.value = false;
  isEmbassy.value = true;
}
const i18n = useI18n();
const changeLanguage = (locale) => {
  i18n.locale.value = locale
}
</script>
<style lang="css" scoped>
.container {
  height: 100vh;
}

h3 {
  margin-top: 20px;
  margin-bottom: 20px;
}

header {
  padding: 5px;
  display: flex;
  background-color: #E30613;
  /* Black (Egyptian flag color) */
  color: #FFFFFF;
  /* White text for readability */
  border-bottom: 3px solid white;
  /* Gold border at the bottom */
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.5);
  /* Subtle shadow */
}

.header-img {
  flex: 1;
  max-width: 52px;
  background: white;
  border-radius: 50%;
  padding: 10px;
}

.header-title {
  flex: 10;
  display: flex;
  align-items: center;
  font-weight: bold;
  font-size: 1.2rem;
}

.header-translate {
  flex: 1;
  display: flex;
  align-items: center;
}

.translate-img {
  border-radius: 50%;
  height: 22px;
  cursor: pointer;
}

.main-content {
  display: flex;
}

nav {

  padding: 10px;
  height: 100vh;
  background-color: #000000;
  width: 250px;
}

.list-item {
  height: 40px;
  padding: 10px;
  color: white;
  font-weight: bold;
  cursor: pointer;
  transition: all 0.3s ease;
}

.list-item:hover {
  background-color: #E30613;
  /* Red (Egyptian flag color) */
  transform: translateX(5px);
  /* Subtle movement effect */
}

.viewer {
  flex: 10;
  padding: 20px;

}

.description {
  line-height: 2rem;
}

.alert {
  padding: 20px;
  font-weight: bold;
  margin-top: 20px;
  ;
}
</style>
