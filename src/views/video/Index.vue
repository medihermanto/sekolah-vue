<template>
    <div id="video">
        <Header/>
        <div id="banner-area" class="banner-area" style="background-image:url(/assets/images/banner/banner3.jpg)">
                <div class="banner-text">
                    <div class="container">
                        <div class="row">
                        <div class="col-lg-12">
                            <div class="banner-heading">
                                <h1 class="banner-title">videos</h1>
                                <nav aria-label="breadcrumb">
                                    <ol class="breadcrumb bg-transparent justify-content-center">
                                        <li class="breadcrumb-item"><router-link :to="{name:'home'}">Home</router-link></li>
                                    <li class="breadcrumb-item"><router-link :to="{name:'video'}">videos</router-link></li>
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
            <h3 class="widget-title">Video</h3>
            <div v-if="videos.length > 0 ">
                <div class="row">
                    <div class="col-lg-6 col-md-6 mb-4" v-for="video in videos" :key="video.id">
                        <div class="latest-post">
                            <div class="latest-post-media">
                                <iframe
                                    style="width:100%;height:300px;border-top-left-radius:.3rem;border-top-right-radius:.3rem"
                                    :src="video.embed" frameborder="0"
                                    allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture"
                                    allowfullscreen></iframe>
                            </div>
                            <div class="post-body">
                            <div class="latest-post-meta text-center">
                                <span class="post-item-date">
                                    <h4>{{ video.title }}</h4> 
                                </span>
                            </div>
                            </div>
                        </div><!-- Latest post end -->
                    </div><!-- 1st post col end -->
                </div>
            </div>
            <div v-else>
                <div class="row">
                    <div class="col-lg-4" v-for="loader in videos_loader" :key="loader">
                        <ContentLoader/>
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
    ContentLoader
} from 'vue-content-loader';

import axios from 'axios';
import {ref,onMounted} from 'vue';

import Header from '../../components/Header.vue';
import Footer from '../../components/Footer.vue';

    export default {
        name: 'VideoComponent',

        components: {
            Header,
            Footer,
            ContentLoader,
        },

        setup() {
            const videos = ref([]);
            const videos_loader = ref(6);

            let moreExists = ref(false);
            let nextPage = ref(0);

            
            const fetchDataVideos = () => {
                axios.get('api/video')
                .then(response => {
                    videos.value = response.data.data.data
                    if(response.data.data.current_page < response.data.data.last_page) {
                        moreExists.value = true
                        nextPage.value = response.data.data.current_page + 1
                    }else{
                        moreExists.value = false
                    }
                })
            }

            const loadMore = () => {
                axios.get(`/api/video?page=${nextPage.value}`)
                .then(response => {
                    if(response.data.data.current_page < response.data.data.last_page) {
                        moreExists.value = true
                        nextPage.value = response.data.data.current_page + 1
                    }else{
                        moreExists.value = false
                    }

                    response.data.data.data.forEach(data => {
                        videos.value.push(data)
                    })
                })
            };

            onMounted(() => {
                fetchDataVideos()
            });

            return {
                videos,
                videos_loader,
                moreExists,
                nextPage,
                loadMore
            }
        }

    }
</script>