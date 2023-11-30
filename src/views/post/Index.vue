<template>
    <div id="post-index">
        <Header/>
<div id="banner-area" class="banner-area" style="background-image:url(assets/images/banner/banner3.jpg)">
  <div class="banner-text">
    <div class="container">
        <div class="row">
          <div class="col-lg-12">
              <div class="banner-heading">
                <h1 class="banner-title">News</h1>
                <nav aria-label="breadcrumb">
                    <ol class="breadcrumb bg-transparent justify-content-center">
                      <li class="breadcrumb-item"><router-link :to="{name:'home'}">Home</router-link></li>
                      <li class="breadcrumb-item"><router-link :to="{name:'post'}">News</router-link></li>
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
            <h3 class="widget-title">Latest Posts</h3>
            <div v-if="posts.length > 0 ">
                <div class="row">
                    <div class="col-lg-4 col-md-6 mb-4" v-for="post in posts" :key="post.id">
                        <div class="latest-post">
                            <div class="latest-post-media">
                            <a href="news-single.html" class="latest-post-img">
                                <img loading="lazy" class="img-fluid" :src="post.image" alt="img">
                            </a>
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

import {ref, onMounted} from 'vue';

import Header from "../../components/Header.vue";
import Footer from "../../components/Footer.vue";
    export default {
        name: 'PostComponent',

        components: {
            FacebookLoader,
            Header,
            Footer,
        },
    setup(){
        const posts = ref([]);
        const posts_loader = ref(6);
        
        let moreExists = ref(false);
        let nextPage = ref(0);

        const fetchDataPosts = () => {
            axios.get('/api/post')
            .then(response => {
                posts.value = response.data.data.data
                if(response.data.data.current_page < response.data.data.last_page){
                    moreExists.value = true

                    nextPage.value = response.data.data.current_page + 1
                }else{
                    moreExists.value = false
                }
            })
        };

        const loadMore = () => {
            axios.get(`/api/post?page=${nextPage.value}`)
            .then(response => {
                
                if(response.data.data.current_page < response.data.data.last_page) {
                    
                    moreExists = true
                    nextPage = response.data.data.current_page + 1
                }else{
                    moreExists.value = false
                }
                response.data.data.data.forEach(data => {
                    posts.value.push(data)
                })
            })
        };

        onMounted(() => {
            fetchDataPosts()
        });



        return {
            posts,
            posts_loader,
            moreExists,
            nextPage,
            loadMore
        }
    }
   
}

</script>