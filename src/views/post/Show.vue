<template>
    <div id="post-index">
        <Header/>
<div id="banner-area" class="banner-area" style="background-image:url(assets/images/banner/banner1.jpg)">
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
                      <li class="breadcrumb-item active" aria-current="page">{{ post.title }}</li>
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
        <div v-if="post.title">
            <div class="post-content post-single">
                
                <h2 class="entry-title text-left" style="color:indigo">
                    {{post.title}}
                </h2>
                <div class="post-meta">
                    <span class="post-author">
                    <i class="far fa-user"></i><a href="#"> Admin</a>
                    </span>
                    <span class="post-cat">
                    <i class="far fa-folder-open"></i><router-link :to="{name:'post'}">News</router-link>
                    </span>
                    <span class="post-meta-date"><i class="far fa-calendar"></i> {{ post.created_at }}</span>
                    <span class="post-comment"><i class="far fa-comment"></i> 03<a href="#"
                        class="comments-link">Comments</a></span>
                </div>
            <div class="post-media post-image">
                <img loading="lazy" :src="post.image" class="img-fluid rounded" alt="post-image">
            </div>
            <div class="post-body">
               <div class="table-responsive">
                    <div class="entry-content" v-html="post.content">
                    </div>
                </div>

                <div class="tags-area d-flex align-items-center justify-content-between">
                <div class="post-tags">
                    <a href="#">Construction</a>
                    <a href="#">Safety</a>
                    <a href="#">Planning</a>
                </div>
                <div class="share-items">
                    <ul class="post-social-icons list-unstyled">
                    <li class="social-icons-head">Share:</li>
                    <li><a href="#"><i class="fab fa-facebook-f"></i></a></li>
                    <li><a href="#"><i class="fab fa-twitter"></i></a></li>
                    <li><a href="#"><i class="fab fa-google-plus"></i></a></li>
                    <li><a href="#"><i class="fab fa-linkedin"></i></a></li>
                    </ul>
                </div>
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
          <div class="widget recent-posts">
            <h3 class="widget-title">Recent Posts</h3>
            <ul class="list-unstyled">
              <div v-if="posts.length > 0">
                <li class="d-flex align-items-center" v-for="post in posts" :key="post.id">
                <div class="posts-thumb">
                  <a href="#"><img loading="lazy" alt="img" :src="post.image"></a>
                </div>
                <div class="post-info">
                  <h4 class="entry-title">
                    <router-link :to="{name: 'detail_post', params: {slug: post.slug}}">{{ post.title }}</router-link>
                   
                  </h4>
                  <p><i class="fa fa-calendar"></i> {{ post.created_at }}</p>
                </div>
              </li><!-- 1st post end-->
              </div>
              <div v-else>
                <div v-for="loader in posts_loader" :key="loader">
                    <FacebookLoader/>
                </div>
              </div>
            </ul>
          </div><!-- Recent post end -->

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

          <div class="widget">
            <h3 class="widget-title">Events </h3>
            <ul class="arrow nav nav-tabs" v-if="events.length > 0">
              <li v-for="event in events" :key="event.id"><router-link :to="{name: 'detail_event', params:{slug: event.slug}}">{{event.title}}6</router-link></li>
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
    FacebookLoader,
    BulletListLoader,
} from 'vue-content-loader';

import axios from 'axios';

import { ref, onMounted, watch } from 'vue';
import { useRoute } from 'vue-router';

import Header from '../../components/Header.vue';
import Footer from '../../components/Footer.vue';

    export default {
        name: 'PostDetailComponent',

        components: {
            FacebookLoader,
            BulletListLoader,

            Header,
            Footer
        },

        setup() {
            const post = ref({});
            const events = ref([]);
            const categories = ref([]);
            const events_loader = ref(2);
            const categories_loader = ref(1);
            const posts = ref([]);
            const posts_loader = ref(3);

            const route = useRoute();

            onMounted(() => {
                // get post detail
                axios.get(`/api/post/${route.params.slug}`)
                .then(response => {
                    post.value = response.data.data;
                })

                // get data posts
                axios.get('/api/homepage/post')
                .then(response => {
                  posts.value = response.data.data;
                })

                // get agenda
                axios.get(`/api/homepage/event`)
                .then(response => {
                    events.value = response.data.data;
                })
                // get kategori
                axios.get(`/api/category`)
                .then(response => {
                    categories.value = response.data.data.data;
                })
            })

            const fetchDataPostBySlug = () => {  axios.get(`/api/post/${route.params.slug}`)
                  .then(response => {
                      post.value = response.data.data;
                  })
                }

            watch(() => route.params.slug, () => {
              fetchDataPostBySlug();
            })

            return {
                post,
                events,
                categories,
                events_loader,
                categories_loader,
                posts,
                posts_loader,
            }
        }
    }
</script>