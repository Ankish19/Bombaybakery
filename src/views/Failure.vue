/* eslint-disable */
<template>
  <div class="failure">
    <Headbar></Headbar>
    <!-- Content -->
    <div id="content">
      <!-- Page Title -->
      <section class="section section-bg-edge text-left mt-5 mb-5 mx-auto">
        <div class="container mt-5 mb-5">
          <div class="row">
            <div class="col-md-12 text-center mt-5">
              <img src="@/assets/failure.png" class="failbg mt-5" alt="" />
            </div>
            <div class="col-md-12">
              <h2
                class="font-weight-bold text-center mb-5"
                style="margin-top: 106px"
              >
                Failure
              </h2>
            </div>
          </div>
        </div>
      </section>
    </div>
    <!-- Content / End -->
    <Footer></Footer>
  </div>
</template>
<script>
/* eslint-disable */
import Headbar from "@/views/layouts/Headbar.vue";
import Footer from "@/views/layouts/Footer.vue";

export default {
  methods: {},
  name: "failure",
  components: {
    Headbar,
    Footer
  },
  mounted () {
    localStorage.removeItem('submitOrder')
  }
}
</script>
