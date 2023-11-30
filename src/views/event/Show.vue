<template>
    <div id="event-detail">
        <Header/>
<div id="banner-area" class="banner-area" style="background-image:url(/assets/images/banner/banner1.jpg)">
  <div class="banner-text">
    <div class="container">
        <div class="row">
          <div class="col-lg-12">
              <div class="banner-heading">
                <h1 class="banner-title">Events</h1>
                <nav aria-label="breadcrumb">
                    <ol class="breadcrumb bg-transparent justify-content-center">
                        <li class="breadcrumb-item"><router-link :to="{name:'home'}">Home</router-link></li>
                      <li class="breadcrumb-item"><router-link :to="{name:'event'}">Events</router-link></li>
                      <li class="breadcrumb-item active" aria-current="page">{{ events.title }}</li>
                    </ol>
                </nav>
              </div>
          </div><!-- Col end -->
        </div><!-- Row end -->
    </div><!-- Container end -->
  </div><!-- Banner text end -->
</div><!-- Banner area end --> 
<section id="main-container" class="main-container">
  <div class="container">
    <div class="row">
      <div class="col-lg-8 mb-5 mb-lg-0">
        <div v-if="events.length > 0">
            <div class="post-content post-single">
                
                <h2 class="entry-title text-left" style="color:indigo">
                    {{event.title}}
                </h2>
                <div class="post-body">
                  <div class="table-responsive">
                    <table class="table table-bordered table-striped">
                        <tr>
                            <th>Lokasi</th>
                            <th><i class="fa fa-map-marker" aria-hidden="true"></i> {{ event.location }}</th>
                        </tr>
                        <tr>
                            <th>Tanggal</th>
                            <th><i class="fa fa-calendar" aria-hidden="true"></i> {{ event.date }}</th>
                        </tr>
                    </table>
                  </div>

             

                </div><!-- post-body end -->
            </div><!-- post content end -->
        </div>
        <div v-else>
            <div class="rounded">
                <FacebookLoader/>
            </div>
        </div>

      </div><!-- Content Col end -->

      <div class="col-lg-4">

        <div class="sidebar sidebar-right">
            <div class="widget">
            <h3 class="widget-title">Other Events </h3>
            <ul class="arrow nav nav-tabs" v-if="events.length > 0">
              <li v-for="event in events" :key="event.id">
                <router-link :to="{name: 'detail_event', params:{slug: event.slug}}">{{event.title}}
                </router-link>
            </li>
            </ul>
            <div v-else>
                <div v-for="loader in events_loader" :key="loader">
                    <FacebookLoader/>
                </div>
            </div>
          </div><!-- Archives end -->
        </div><!-- Sidebar end -->
      </div><!-- Sidebar Col end -->

    </div><!-- Main row end -->

  </div><!-- Conatiner end -->
</section><!-- Main container end -->
<Footer/>
    </div>
</template>


<script>
import {
    FacebookLoader
} from 'vue-content-loader';

import axios from 'axios';
import { ref, onMounted, watch} from 'vue';

import { useRoute } from 'vue-router';

    import Header from '../../components/Header.vue';
    import Footer from '../../components/Footer.vue';

    export default {
        name: 'EventDetailComponent',

        components: {
            FacebookLoader,
            Header,
            Footer
        },

        setup() {
            const event = ref({});
            const events = ref([]);
            const events_loader = ref(2);
            const categories = ref([]);

            const route = useRoute();

            onMounted(() => {
                axios.get(`/api/event/${route.params.slug}`)
                .then(response => {
                    event.value = response.data.data
                })

                axios.get('/api/homepage/event')
                .then(response => {
                    events.value = response.data.data
                    
                })
            })

            const fetchDataEventsBySlug = () => {
                axios.get(`/api/event/${route.params.slug}`)
                .then(response => {
                    event.value = response.data.data
                })
            }

            watch(() => route.params.slug, () => {
                fetchDataEventsBySlug();
            })

            return {
                event,
                events,
                events_loader,
                categories,
            }
        }
    }
</script>