<template>
    <div id="contact">
        <Header/>
        <div id="banner-area" class="banner-area" style="background-image:url(/assets/images/banner/banner3.jpg)">
                <div class="banner-text">
                    <div class="container">
                        <div class="row">
                        <div class="col-lg-12">
                            <div class="banner-heading">
                                <h1 class="banner-title">contact</h1>
                                <nav aria-label="breadcrumb">
                                    <ol class="breadcrumb bg-transparent justify-content-center">
                                        <li class="breadcrumb-item"><router-link :to="{name:'home'}">Home</router-link></li>
                                    <li class="breadcrumb-item"><router-link :to="{name:'contact'}">contact</router-link></li>
                                   
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
                    <h3 class="widget-title">CONTACT</h3>
                <div class="col-lg-8 mb-5 mb-lg-0">
                    <div class="post">
                       <div class="card">
                        <div class="card-body">
                            <iframe src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3981.9588362427335!2d98.67865677591128!3d3.5969086502350986!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x303131c066266873%3A0xa1d01517079235b9!2sUniversitas%20HKBP%20Nommensen%20Medan!5e0!3m2!1sid!2sid!4v1699101292112!5m2!1sid!2sid" width="100%" height="450" style="border:0;" 
                            allowfullscreen="" loading="lazy" referrerpolicy="no-referrer-when-downgrade"></iframe>
                        </div>
                       </div>
                    </div>
                </div><!-- Content Col end -->
                
                <div class="col-lg-4">
                <div class="sidebar sidebar-right">
                    <div class="widget">
                                <h3>ALAMAT</h3>
                                <div class="post-body">
                                    <div class="latest-post-meta">
                                        <span class="post-item-date">
                                            <h4>Universitas HKBP Nommensen Medan</h4>
                                            <p>
                                                <i class="fa fa-map-marker" aria-hidden="true"></i> Jl. Sutomo No.4A, Perintis, Kec. Medan Tim., Kota Medan, Sumatera Utara 20235
                                            </p>
                                            <p><i class="fa fa-phone"></i> (061) 4522922</p>
                                            <p><i class="fa fa-globe"></i><a href="http://uhn.ac.id" target="_blank"> uhn.ac.id</a> </p>
                                            <p><i class="fas fa-envelope"></i> admin@uhn.ac.id</p>
                                        </span>
                                    </div>
                                    </div>
                    </div><!-- Categories end -->
                </div><!-- Sidebar end -->
            </div><!-- Sidebar Col end -->

            </div><!-- Main row end -->

            </div><!-- Container end -->
        </section><!-- Main container end -->
        <Footer/>
    </div>
</template>

<script>
import Header from '../../components/Header.vue';
import Footer from '../../components/Footer.vue';

    export default {
    name: 'ContactComponent',
    components: { Header, Footer }
}
</script>