<template>
     <footer id="footer" class="footer bg-overlay">
        <div class="footer-main">
          <div class="container">
            <div class="row justify-content-between">
              <div class="col-lg-4 col-md-6 footer-widget footer-about">
                <h3 class="widget-title">About Us</h3>
                <img loading="lazy" class="footer-logo" :src="logoPath" alt="Constra">
                <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor inci done idunt ut
                  labore et dolore magna aliqua.</p>
                <div class="footer-social">
                  <ul>
                    <li><a href="https://facebook.com/themefisher" aria-label="Facebook"><i
                          class="fab fa-facebook-f"></i></a></li>
                    <li><a href="https://twitter.com/themefisher" aria-label="Twitter"><i class="fab fa-twitter"></i></a>
                    </li>
                    <li><a href="https://instagram.com/themefisher" aria-label="Instagram"><i
                          class="fab fa-instagram"></i></a></li>
                    <li><a href="https://github.com/themefisher" aria-label="Github"><i class="fab fa-github"></i></a></li>
                  </ul>
                </div><!-- Footer social end -->
              </div><!-- Col end -->
    
              <div class="col-lg-4 col-md-6 footer-widget mt-5 mt-md-0">
                <div class="widget widget-tags">
                  <h3 class="widget-title">Tags </h3>
                  <div v-if="tags.length > 0">
                      <router-link :to="{name: 'detail_tag', params: { slug: tag.slug }}" class="btn btn-sm btn-outline-secondary text-white m-2" v-for="tag in tags" :key="tag.id">{{ tag.name }}</router-link>
                  </div>
                </div><!-- Tags end -->
                <!-- <h3 class="widget-title">Working Hours</h3>
                <div class="working-hours">
                  We work 7 days a week, every day excluding major holidays. Contact us if you have an emergency, with our
                  Hotline and Contact form.
                  <br><br> Monday - Friday: <span class="text-right">10:00 - 16:00 </span>
                  <br> Saturday: <span class="text-right">12:00 - 15:00</span>
                  <br> Sunday and holidays: <span class="text-right">09:00 - 12:00</span>
                </div> -->
              </div><!-- Col end -->
    
              <div class="col-lg-3 col-md-6 mt-5 mt-lg-0 footer-widget">
                <h3 class="widget-title">Services</h3>
                <ul class="list-arrow">
                  <li><a href="service-single.html">Pre-Construction</a></li>
                  <li><a href="service-single.html">General Contracting</a></li>
                  <li><a href="service-single.html">Construction Management</a></li>
                  <li><a href="service-single.html">Design and Build</a></li>
                  <li><a href="service-single.html">Self-Perform Construction</a></li>
                </ul>
              </div><!-- Col end -->
            </div><!-- Row end -->
          </div><!-- Container end -->
        </div><!-- Footer main end -->
    
        <div class="copyright">
          <div class="container">
            <div class="row align-items-center">
              <div class="col-md-12">
                <div class="copyright-info text-center">
                  <span>Copyright &copy; 2023, Designed &amp; Developed by <a href="https://mhtdev.my.id">MHT</a></span>
                </div>
              </div>
            </div><!-- Row end -->
    
            <div id="back-to-top" data-spy="affix" data-offset-top="10" class="back-to-top position-fixed">
              <button class="btn btn-primary" title="Back to Top">
                <i class="fa fa-angle-double-up"></i>
              </button>
            </div>
    
          </div><!-- Container end -->
        </div><!-- Copyright end -->
      </footer><!-- Footer end -->
</template>

<script>
    //import content loader
    import {
        ListLoader
    } from 'vue-content-loader';

    //import axios
    import axios from 'axios';

    //import hook onMounted from vue
    import { ref, onMounted } from 'vue';

    export default {
        name: 'FooterComponent',

        computed: {
          logoPath() {
            return new URL(`/assets/images/footer-logo.png`, import.meta.url).href;
          }
        },

        components: {
            //loader component
            ListLoader
        },
        
        setup() {
            
            //define state
            const tags = ref([]);

            //on mounted
            onMounted(() => {
                axios.get('/api/tag')
                    .then(response => {
                        tags.value = response.data.data.data;
                    })
                    .catch(() => {
                        tags.value = [];
                    });
            })

            //return data
            return {
                tags,
            }
        }
    }
</script>