<template>
    <div id="home">
        <Header />
        <Slider />
       
        <!-- start homepage -->
    <section class="call-to-action no-padding">
      <div class="container">
        <div class="action-style-box">
            <div class="row align-items-center">
              <div class="col-md-12 text-center text-md-left">
                  <div class="call-to-action-text">
                    <h3 class="action-title">Sekolah dengan fasilitas yang memadai, berbasis digital dan memiliki Akreditasi A, serta mampu mencetak generasi unggul, berdaya saing</h3>
                    
                </div>
              </div><!-- Col end -->
            </div><!-- row end -->
        </div><!-- Action style box -->
      </div><!-- Container end -->
    </section><!-- Action end -->
    
    <section id="ts-features" class="ts-features">
      <div class="container">
        <div v-if="profiles.length > 0">
            <div v-for="profile in profiles" :key="profile.id">
                <div class="row">
                    <div class="col-lg-6">
                    <div class="ts-intro">
                        <h3 class="into-sub-title">Sambutan Pimpinan</h3>
                        <p v-html="profile.opening_speech"></p>
                    </div><!-- Intro box end -->
                    </div><!-- Col end -->
                    <div class="col-lg-6">
                        <img :src="profile.image"
                    class="w-100" style="height:500px;object-fit:cover" >
                    </div><!-- Col end -->
                </div>
            </div>
        </div><!-- Row end -->
        <div v-else>
            <div class="row">
                <div class="col-6">
                <FacebookLoader/>
            </div>
            <div class="col-6">
                <FacebookLoader/>
            </div>
            </div>
        </div>
      </div><!-- Container end -->
    </section><!-- Feature are end -->
    
    <section id="facts" class="facts-area dark-bg">
      <div class="container">
        <div class="facts-wrapper">
            <div class="row">
                <div class="col-md-6 col-sm-6 ts-facts" v-if="teachers.length > 0">
                    <div class="ts-facts-img">
                        <img loading="lazy" src="assets/images/icon-image/professor.png" alt="facts-img">
                    </div>
                    <div class="ts-facts-content" >
                        <h2 class="ts-facts-num"><vue3-autocounter ref='counter' :startAmount='0' :endAmount='teachers.length' :duration='2' /></h2>
                        <h3 class="ts-facts-title">Teachers</h3>
                    </div>
                </div>
                <!-- Col end -->
                <div class="col-md-6 col-sm-6 ts-facts" v-if="students.length > 0">
                    <div class="ts-facts-img">
                        <img loading="lazy" src="assets/images/icon-image/professor.png" alt="facts-img">
                    </div>
                    <div class="ts-facts-content">
                        <h2 class="ts-facts-num"><vue3-autocounter ref='counter' :startAmount='0' :endAmount='students.length' :duration='2' /></h2>
                        
                        <h3 class="ts-facts-title">Students</h3>
                    </div>
                </div><!-- Col end -->   
                <div v-else>
                   <div class="row">
                    <div class="col-6">
                      <FacebookLoader/>
                    </div>
                    <div class="col-6">
                      <FacebookLoader/>
                    </div>
                   </div>
                </div>
            </div> <!-- Facts end -->
        </div>
        <!--/ Content row end -->
      </div>
      <!--/ Container end -->
    </section><!-- Facts end -->
    
    <section id="ts-service-area" class="ts-service-area pb-0">
      <div class="container">
        <div class="row text-center">
            <div class="col-12">
              <h2 class="section-title">We Are Specialists In</h2>
              <h3 class="section-sub-title">What We Do</h3>
            </div>
        </div>
        <!--/ Title row end -->
    
        <div class="row">
            <div class="col-lg-4">
              <div class="ts-service-box d-flex">
                  <div class="ts-service-box-img">
                    <img loading="lazy" src="assets/images/icon-image/service-icon1.png" alt="service-icon">
                  </div>
                  <div class="ts-service-box-info">
                    <h3 class="service-box-title"><a href="#">Home Construction</a></h3>
                    <p>Lorem ipsum dolor sit amet consectetur adipiscing elit Integer adipiscing erat</p>
                  </div>
              </div><!-- Service 1 end -->
    
              <div class="ts-service-box d-flex">
                  <div class="ts-service-box-img">
                    <img loading="lazy" src="assets/images/icon-image/service-icon2.png" alt="service-icon">
                  </div>
                  <div class="ts-service-box-info">
                    <h3 class="service-box-title"><a href="#">Building Remodels</a></h3>
                    <p>Lorem ipsum dolor sit amet consectetur adipiscing elit Integer adipiscing erat</p>
                  </div>
              </div><!-- Service 2 end -->
    
              <div class="ts-service-box d-flex">
                  <div class="ts-service-box-img">
                    <img loading="lazy" src="assets/images/icon-image/service-icon3.png"  alt="service-icon">
                  </div>
                  <div class="ts-service-box-info">
                    <h3 class="service-box-title"><a href="#">Interior Design</a></h3>
                    <p>Lorem ipsum dolor sit amet consectetur adipiscing elit Integer adipiscing erat</p>
                  </div>
              </div><!-- Service 3 end -->
    
            </div><!-- Col end -->
    
            <div class="col-lg-4 text-center">
              <img loading="lazy" class="img-fluid" src="assets/images/services/service-center.jpg" alt="service-avater-image">
            </div><!-- Col end -->
    
            <div class="col-lg-4 mt-5 mt-lg-0 mb-4 mb-lg-0">
              <div class="ts-service-box d-flex">
                  <div class="ts-service-box-img">
                    <img loading="lazy" src="assets/images/icon-image/service-icon4.png" alt="service-icon">
                  </div>
                  <div class="ts-service-box-info">
                    <h3 class="service-box-title"><a href="#">Exterior Design</a></h3>
                    <p>Lorem ipsum dolor sit amet consectetur adipiscing elit Integer adipiscing erat</p>
                  </div>
              </div><!-- Service 4 end -->
    
              <div class="ts-service-box d-flex">
                  <div class="ts-service-box-img">
                    <img loading="lazy" src="assets/images/icon-image/service-icon5.png" alt="service-icon">
                  </div>
                  <div class="ts-service-box-info">
                    <h3 class="service-box-title"><a href="#">Renovation</a></h3>
                    <p>Lorem ipsum dolor sit amet consectetur adipiscing elit Integer adipiscing erat</p>
                  </div>
              </div><!-- Service 5 end -->
    
              <div class="ts-service-box d-flex">
                  <div class="ts-service-box-img">
                    <img loading="lazy" src="assets/images/icon-image/service-icon6.png" alt="service-icon">
                  </div>
                  <div class="ts-service-box-info">
                    <h3 class="service-box-title"><a href="#">Safety Management</a></h3>
                    <p>Lorem ipsum dolor sit amet consectetur adipiscing elit Integer adipiscing erat</p>
                  </div>
              </div><!-- Service 6 end -->
            </div><!-- Col end -->
        </div><!-- Content row end -->
    
      </div>
      <!--/ Container end -->
    </section><!-- Service end -->
    
<section id="main-container" class="main-container pb-4 solid-bg">
  <div class="container">
    <div class="row text-center">
      <div class="col-lg-12">
        <h3 class="section-sub-title">Our Teachers</h3>
      </div>
    </div>
    <!--/ Title row end -->

    <div class="row justify-content-center" v-if="teachers.length > 0">
      <div class="col-lg-3 col-sm-6 mb-5" v-for="teacher in teachers" :key="teacher.id">
        <div class="ts-team-wrapper">
          <div class="team-img-wrapper">
            <img loading="lazy" :src="teacher.image" style="height:500px" class="img-fluid" alt="team-img">
          </div>
          <div class="ts-team-content-classic">
            <h3 class="ts-name">{{ teacher.name }}</h3>
           <p>{{teacher.position}}</p> 
           <p class="ts-designation" v-for="subject in subjects" :key="subject.id">
            <!-- <div v-if="teacher.subject_id == subject.id">
            {{ teacher.subject.name }}
            </div> -->
           </p>
            <p class="ts-description"> <i class="fas fa-envelope"></i> {{teacher.email}} <br> <i class="fa fa-phone-square"></i> (+62) {{teacher.phone}}</p>
            <div class="team-social-icons">
              <a target="_blank" href="#"><i class="fab fa-facebook-f"></i></a>
              <a target="_blank" href="#"><i class="fab fa-twitter"></i></a>
              <a target="_blank" href="#"><i class="fab fa-linkedin"></i></a>
            </div>
            <!--/ social-icons-->
          </div>
        </div>
        <!--/ Team wrapper 1 end -->
      </div><!-- Col end -->
    </div><!-- Content row 1 end -->
  </div><!-- Container end -->
</section><!-- Main container end -->

  
    
    <section class="content">
      <div class="container">
        <div class="row">
            <div class="col-lg-6">
              <h3 class="column-title">Testimonials</h3>
    
              <div id="testimonial-slide" class="testimonial-slide">
                  <div class="item">
                    <div class="quote-item">
                        <span class="quote-text">
                          Question ran over her cheek When she reached the first hills of the Italic Mountains, she had a last
                          view back on the skyline of her hometown Bookmarksgrove, the headline of Alphabet Village and the
                          subline of her own road.
                        </span>
    
                        <div class="quote-item-footer">
                          <img loading="lazy" class="testimonial-thumb" src="assets/images/clients/testimonial1.png" alt="testimonial">
                          <div class="quote-item-info">
                              <h3 class="quote-author">Gabriel Denis</h3>
                              <span class="quote-subtext">Chairman, OKT</span>
                          </div>
                        </div>
                    </div><!-- Quote item end -->
                  </div>
                  <!--/ Item 1 end -->
    
                  <div class="item">
                    <div class="quote-item">
                        <span class="quote-text">
                          Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor inci done idunt ut
                          labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitoa tion ullamco laboris
                          nisi aliquip consequat.
                        </span>
    
                        <div class="quote-item-footer">
                          <img loading="lazy" class="testimonial-thumb" src="assets/images/clients/testimonial2.png" alt="testimonial">
                          <div class="quote-item-info">
                              <h3 class="quote-author">Weldon Cash</h3>
                              <span class="quote-subtext">CFO, First Choice</span>
                          </div>
                        </div>
                    </div><!-- Quote item end -->
                  </div>
                  <!--/ Item 2 end -->
    
                  <div class="item">
                    <div class="quote-item">
                        <span class="quote-text">
                          Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor inci done idunt ut
                          labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitoa tion ullamco laboris
                          nisi ut commodo consequat.
                        </span>
    
                        <div class="quote-item-footer">
                          <img loading="lazy" class="testimonial-thumb" src="assets/images/clients/testimonial3.png" alt="testimonial">
                          <div class="quote-item-info">
                              <h3 class="quote-author">Minter Puchan</h3>
                              <span class="quote-subtext">Director, AKT</span>
                          </div>
                        </div>
                    </div><!-- Quote item end -->
                  </div>
                  <!--/ Item 3 end -->
    
              </div>
              <!--/ Testimonial carousel end-->
            </div><!-- Col end -->
    
            <div class="col-lg-6 mt-5 mt-lg-0">
    
              <h3 class="column-title">Happy Clients</h3>
    
              <div class="row all-clients">
                  <div class="col-sm-4 col-6">
                    <figure class="clients-logo">
                        <a href="#!"><img loading="lazy" class="img-fluid" src="assets/images/clients/client1.png" alt="clients-logo" /></a>
                    </figure>
                  </div><!-- Client 1 end -->
    
                  <div class="col-sm-4 col-6">
                    <figure class="clients-logo">
                        <a href="#!"><img loading="lazy" class="img-fluid" src="assets/images/clients/client2.png" alt="clients-logo" /></a>
                    </figure>
                  </div><!-- Client 2 end -->
    
                  <div class="col-sm-4 col-6">
                    <figure class="clients-logo">
                        <a href="#!"><img loading="lazy" class="img-fluid" src="assets/images/clients/client3.png" alt="clients-logo" /></a>
                    </figure>
                  </div><!-- Client 3 end -->
    
                  <div class="col-sm-4 col-6">
                    <figure class="clients-logo">
                        <a href="#!"><img loading="lazy" class="img-fluid" src="assets/images/clients/client4.png" alt="clients-logo" /></a>
                    </figure>
                  </div><!-- Client 4 end -->
    
                  <div class="col-sm-4 col-6">
                    <figure class="clients-logo">
                        <a href="#!"><img loading="lazy" class="img-fluid" src="assets/images/clients/client5.png" alt="clients-logo" /></a>
                    </figure>
                  </div><!-- Client 5 end -->
    
                  <div class="col-sm-4 col-6">
                    <figure class="clients-logo">
                        <a href="#!"><img loading="lazy" class="img-fluid" src="assets/images/clients/client6.png" alt="clients-logo" /></a>
                    </figure>
                  </div><!-- Client 6 end -->
    
              </div><!-- Clients row end -->
    
            </div><!-- Col end -->
    
        </div>
        <!--/ Content row end -->
      </div>
      <!--/ Container end -->
    </section><!-- Content end -->
    
    <section class="subscribe no-padding">
      <div class="container">
        <div class="row">
            <div class="col-lg-4">
              <div class="subscribe-call-to-acton">
                  <h3>Can We Help?</h3>
                  <h4>(+9) 847-291-4353</h4>
              </div>
            </div><!-- Col end -->
    
            <div class="col-lg-8">
              <div class="ts-newsletter row align-items-center">
                  <div class="col-md-5 newsletter-introtext">
                    <h4 class="text-white mb-0">Newsletter Sign-up</h4>
                    <p class="text-white">Latest updates and news</p>
                  </div>
    
                  <div class="col-md-7 newsletter-form">
                    <form action="#" method="post">
                        <div class="form-group">
                          <label for="newsletter-email" class="content-hidden">Newsletter Email</label>
                          <input type="email" name="email" id="newsletter-email" class="form-control form-control-lg" placeholder="Your your email and hit enter" autocomplete="off">
                        </div>
                    </form>
                  </div>
              </div><!-- Newsletter end -->
            </div><!-- Col end -->
    
        </div><!-- Content row end -->
      </div>
      <!--/ Container end -->
    </section>
    <!--/ subscribe end -->
    
    <section id="news" class="news">
      <div class="container">
        <div class="row text-center">
            <div class="col-12">
              <h3 class="section-sub-title">Recent Posts</h3>
            </div>
        </div>
        <!--/ Title row end -->
    
        <div v-if="posts.length > 0" class="row">
            <div class="col-lg-3 col-md-6 mb-4" v-for="post in posts" :key="post.id">
              <div class="latest-post">
                  <div class="latest-post-media">
                    <a href="news-single.html" class="latest-post-img">
                        <img loading="lazy" class="img-fluid" :src="post.image" alt="img">
                    </a>
                  </div>
                  <div class="post-body">
                    <h4 class="post-title">
                      <router-link :to="{name: 'detail_post', params: {slug: post.slug}}">{{post.title}}</router-link>
                    </h4>
                
                    <div class="latest-post-meta">
                        <span class="post-item-date">
                          <i class="fa fa-calendar"></i> {{post.created_at}}
                        </span>
                    </div>
                  </div>
                <div class="general-btn mt-1">
                    <router-link :to="{name: 'detail_post', params: {slug: post.slug}}">Continue Read ...</router-link>
                </div>
              </div><!-- Latest post end -->
            </div><!-- 3rd post col end -->
        </div>

     <div v-else>
        <div class="row">
            <div class="col-lg-4 col-md-6 mb-4" v-for="loader in posts_loader" :key="loader">
            <div class="latest-post">
                <div class="latest-post-media">
                    <FacebookLoader />
                </div>
                <div class="post-body">
                    <FacebookLoader />
                </div>
                <div class="general-btn mt-1">
                    <FacebookLoader />
                </div>
            </div>
            </div>
        </div>
     </div>
        <!--/ Content row end -->
    
        <div class="general-btn text-center mt-4">
            <router-link :to="{name:'post'}"><a class="btn btn-primary">See All Posts</a></router-link>
        </div>
    
      </div>
      <!--/ Container end -->
    </section>
    <!--/ News end -->
        <!-- end homepage -->

        <Footer />
    </div>
</template>

<script>
    import {
        ContentLoader,
        FacebookLoader,
        BulletListLoader,
    } from 'vue-content-loader';

    import axios from 'axios';
    
    import Vue3Autocounter from 'vue3-autocounter';

    import {ref, onMounted} from 'vue';

    import Header from "../../components/Header.vue";
    import Slider from "../../components/Slider.vue";
    import Footer from "../../components/Footer.vue";

    export default {
        name: 'HomeComponent',

        components: {
            'vue3-autocounter': Vue3Autocounter,
            ContentLoader,
            FacebookLoader,
            BulletListLoader,

            Header,
            Slider,
            Footer
        },


        setup() {
            const teachers = ref([]);
            const teachers_loader = ref(1);
            const students = ref([]);
            const students_loader = ref(1);
            const posts = ref([]);
            const posts_loader = ref(3);
            const videos = ref([]);
            const videos_loader = ref([]);
            const events = ref([]);
            const events_loader = ref(3);
            const categories = ref([]);
            const categories_loader = ref(1);
            const photos = ref([]);
            const photos_loader = ref(2);
            const profiles = ref([]);
            const profiles_loader = ref(1)
            const subjects = ref([]);
            const subjects_loader = ref(1);

            onMounted(() => {
            // get data teachers
            axios.get('api/homepage/teacher')
            .then(response => {
              teachers.value = response.data.data;
            })
            // get data subjects
            axios.get('api/homepage/subject')
            .then(response => {
              subjects.value = response.data.data;
            })

            // get data students
            axios.get('api/homepage/student')
            .then(response => {
                students.value = response.data.data;
            })
            // get data profiles
            axios.get('/api/homepage/profile')
            .then(response => {
                profiles.value = response.data.data;
            })
            // get data posts
            axios.get('/api/homepage/post')
            .then(response => {
                posts.value = response.data.data;
            })
            // get data videos
            axios.get('/api/homepage/video')
            .then(response => {
                videos.value = response.data.data;
            })
            //get events
            axios.get('/api/homepage/event')
            .then(response => {
                events.value = response.data.data;
            })

            //get categories
            axios.get('/api/category')
                .then(response => {
                    categories.value = response.data.data.data;
                })

            //get photos
            axios.get('/api/homepage/photo')
                .then(response => {
                    photos.value = response.data.data;
                })
            
        });

        return {
            teachers,
            teachers_loader,
            students,
            students_loader,
            posts,
            posts_loader,
            videos,
            videos_loader,
            events,
            events_loader,
            categories,
            categories_loader,
            photos,
            photos_loader,
            profiles,
            profiles_loader,
            subjects,
            
        }
        }
    }
</script>