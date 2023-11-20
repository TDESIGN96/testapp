<template>
  <div v-if="invoicesLoaded">
    <div  class="app flex flex-column">
      <Navigation />

      <div class="app-content flex flex-column">
        <Modal v-if="modalActive" />
        <transition name="invoice">
          <InvoiceModal v-if="invoiceModal" />
        </transition>
        <Nuxt />
        <Footer />
      </div>
    </div>
  </div>
</template>

<script>
import { mapState, mapActions } from 'vuex';

export default {
  data() {
    return {
      isMobile: false,
    };
  },
  computed: {
    ...mapState(['invoiceModal', 'modalActive', 'invoicesLoaded']),
  },
  mounted() {
    this.checkScreen();
    window.addEventListener('resize', this.checkScreen);
  },
  methods: {
    ...mapActions(['GET_INVOICES']),
    checkScreen() {
      const windowWidth = window.innerWidth;
      if (windowWidth < 1) {
        this.isMobile = true;
      } else {
        this.isMobile = false;
      }
    },
  },
};
</script>
