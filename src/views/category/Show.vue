<template>
    <div id="category">
        <Header/>
            <div id="banner-area" class="banner-area" style="background-image:url(/assets/images/banner/banner3.jpg)">
                <div class="banner-text">
                    <div class="container">
                        <div class="row">
                        <div class="col-lg-12">
                            <div class="banner-heading">
                                <h1 class="banner-title">news</h1>
                                <nav aria-label="breadcrumb">
                                    <ol class="breadcrumb bg-transparent justify-content-center">
                                        <li class="breadcrumb-item"><router-link :to="{name:'home'}">Home</router-link></li>
                                    <li class="breadcrumb-item"><router-link :to="{name:'post'}">news</router-link></li>
                                    <li class="breadcrumb-item">{{categoryInfo.message}}</li>
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
                    <div class="post">
                        <h3 class="widget-title" style="color:indigo">{{categoryInfo.message}}</h3>
                        <div v-if="posts.length > 0 ">
                            <div class="row">
                                <div class="col-lg-6 col-md-6 mb-4" v-for="post in posts" :key="post.id">
                                    <div class="latest-post">
                                        <div class="latest-post-media">
                                        <router-link :to="{name: 'detail_post', params: {slug: post.slug}}" class="latest-post-img">
                                            <img loading="lazy" class="img-fluid" :src="post.image" alt="img">
                                        </router-link>
                                        </div>
                                        <div class="post-body">
                                            <router-link :to="{name: 'detail_post', params: {slug: post.slug}}" class="text-dark text-decoration-none">
                                        <h4 class="post-title">
                                            {{ post.title }}
                                        </h4></router-link>
                                        <div class="latest-post-meta">
                                            <span class="post-item-date">
                                                <i class="fa fa-calendar"></i> {{ post.created_at }}
                                            </span>
                                        </div>
                                        </div>
                                    </div><!-- Latest post end -->
                                </div><!-- 1st post col end -->
                            </div>
                        </div>
                        <div v-else>
                            <div class="row">
                               <div class="alert alert-danger">
                                <strong>DATA BERITA TIDAK DITEMUKAN !</strong>
                               </div>
                            </div>
                        </div>
                    </div>
                </div><!-- Content Col end -->
                
                <div class="col-lg-4">
                <div class="sidebar sidebar-right">
                    <div class="widget">
                        <h3 class="widget-title">Categories</h3>
                        <div v-if="categories.length > 0">
                            <ul class="arrow nav nav-tabs">
                                <li v-for="category in categories" :key="category.id"><router-link :to="{name: 'detail_category', params:{slug: category.slug}}">{{category.name}}</router-link></li>               
                            </ul>
                        </div>
                        <div v-else>
                            <div v-for="loader in categories_loader" :key="loader">
                            <FacebookLoader/>
                            </div>
                        </div>
                    </div><!-- Categories end -->
                </div><!-- Sidebar end -->
            </div><!-- Sidebar Col end -->

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

import { FacebookLoader } from 'vue-content-loader';

import axios from 'axios';
import {ref, onMounted, watch} from 'vue';

import Header from '../../components/Header.vue';
import Footer from '../../components/Footer.vue';

import { useRoute } from 'vue-router';

    export default {
    name: 'CategoryComponent',
    components: { 
        FacebookLoader,
        Header, 
        Footer 
    },

    setup() {
        const posts = ref([]);
        const categoryInfo = ref({});
        const categories = ref([]);
        let moreExists = ref(false);
        let nextPage = ref(0);
        const categories_loader = ref(1);

        const route = useRoute();

        const fetchDataPostsByCategory = () => {
            axios.get(`/api/category/${route.params.slug}`)
            .then(response => {
                categoryInfo.value = response.data.response
                posts.value = response.data.data.data

                if(response.data.data.current_page < response.data.data.last_page){
                    moreExists.value = true

                    nextPage.value = response.data.data.current_page + 1
                }else{
                    moreExists.value = false
                }
            })
        }

        const loadMore = () => {
            axios.get(`/api/category/${route.params.slug}?page=${nextPage.value}`)
            .then(response => {
                if (response.data.data.current_page < response.data.data.last_page) {
                    moreExists.value = true

                    nextPage.value = response.data.data.current_page + 1
                }else{
                    moreExists.value = false
                }

                response.data.data.data.forEach(data => {
                    posts.value.push(data)
                })
            })
        }

        const getcategory = () => {
            // get kategori
            axios.get(`/api/category`)
            .then(response => {
                categories.value = response.data.data.data;
            })
        }

        onMounted(() => {
            fetchDataPostsByCategory();
            getcategory();
       
        })

        watch(() => route.params.slug, () => {
            fetchDataPostsByCategory();
        })

        return {
            nextPage,
            loadMore,
            posts,
            categoryInfo,
            categories,
            categories_loader
        }
    }

}
</script>

