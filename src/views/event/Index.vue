<template>
    <div id="event">
        <Header/>
<div id="banner-area" class="banner-area" style="background-image:url(assets/images/banner/banner3.jpg)">
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

      <div class="col-lg-12 mb-5 mb-lg-0">
        
        <div class="post">
            <h3 class="widget-title">Latest Events</h3>
            <div v-if="events.length > 0 ">
                <div class="row">
                    <div class="col-lg-4 col-md-6 mb-4" v-for="event in events" :key="event.id">
                        <div class="latest-post">
                            <div class="latest-post-media">
                            </div>
                            <div class="post-body">
                                <router-link :to="{name: 'detail_event', params: {slug: event.slug}}" class="text-dark text-decoration-none">
                            <h4 class="post-title">
                                {{ event.title }}
                            </h4></router-link>
                            <div class="latest-post-meta">
                                <span class="post-item-date">
                                    <i class="fa fa-map-marker"></i> {{ event.location }}
                                </span>
                            </div>
                            <div class="latest-post-meta">
                                <span class="post-item-date">
                                    <i class="fa fa-calendar"></i> {{ event.date }}
                                </span>
                            </div>
                            </div>
                        </div><!-- Latest post end -->
                    </div><!-- 1st post col end -->
                </div>
            </div>
            <div v-else>
                <div class="row">
                    <div class="col-lg-4" v-for="loader in posts_loader" :key="loader">
                        <FacebookLoader/>
                    </div>
                </div>
            </div>
        </div>
      </div><!-- Content Col end -->
      

    </div><!-- Main row end -->
    <div class="text-center" v-show="moreExists">
        <button type="button" class="btn btn-primary btn-sm" v-on:click="loadMore"><span class="fa fa-arrow-down"></span> LOAD MORE</button>
    </div>

  </div><!-- Container end -->
</section><!-- Main container end -->
<Footer/>
    </div>
</template>

<script>
import {
    FacebookLoader
} from 'vue-content-loader';

import axios from 'axios';

import { ref, onMounted } from 'vue';

import Header from "../../components/Header.vue";
import Footer from '../../components/Footer.vue';

    export default {
        name: 'EventComponent',

        components: {
            FacebookLoader,
            Header,
            Footer,
        },
        setup() {
            // define state
            const events = ref([]);
            const events_loader = ref(4);

            // define state moreExists
            let moreExists = ref(false);
            let nextPage = ref(0);

            const fetchDataEvents = () => {
                axios.get('/api/event')
                .then(response => {
                    events.value = response.data.data.data

                    if(response.data.data.current_page < response.data.data.last_page) {
                        moreExists.value = true
                        nextPage.value = response.data.data.current_page +1
                    }else{
                        moreExists.value = false
                    }
                })
            }
            const loadMore = () => {
                axios.get(`/api/event?page=${nextPage.value}`)
                .then(response => {
                    if (response.data.data.current_page < response.data.data.last_page) {
                        moreExists = true

                        nextPage = response.data.data.current_page +1
                    }else{
                        moreExists.value = false
                    }

                    response.data.data.data.forEach(data => {
                        events.value.push(data)
                    })
                })
            }

            onMounted(() => {
                fetchDataEvents()
            });
            return{
                events,
                events_loader,
                moreExists,
                nextPage,
                loadMore
            }
        }
    }
</script>