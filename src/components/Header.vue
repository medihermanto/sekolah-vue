<template>
  <div id="top-bar" class="top-bar">
            <div class="container">
              <div class="row">
                  <div class="col-lg-8 col-md-8">
                    <ul class="top-info text-center text-md-left">
                        <li><i class="fas fa-map-marker-alt"></i> <p class="info-text">9051 Constra Incorporate, USA</p>
                        </li>
                    </ul>
                  </div>
                  <!--/ Top info end -->
      
                  <div class="col-lg-4 col-md-4 top-social text-center text-md-right">
                    <ul class="list-unstyled">
                        <li>
                          <a title="Facebook" href="https://facebbok.com/themefisher.com">
                              <span class="social-icon"><i class="fab fa-facebook-f"></i></span>
                          </a>
                          <a title="Twitter" href="https://twitter.com/themefisher.com">
                              <span class="social-icon"><i class="fab fa-twitter"></i></span>
                          </a>
                          <a title="Instagram" href="https://instagram.com/themefisher.com">
                              <span class="social-icon"><i class="fab fa-instagram"></i></span>
                          </a>
                          <a title="Linkdin" href="https://github.com/themefisher.com">
                              <span class="social-icon"><i class="fab fa-github"></i></span>
                          </a>
                        </li>
                    </ul>
                  </div>
                  <!--/ Top social end -->
              </div>
              <!--/ Content row end -->
            </div>
            <!--/ Container end -->
        </div>
  <header id="header" class="header-one">
      <div class="bg-white">
        <div class="container">
          <div class="logo-area py-2">
              <div class="row align-items-center">
                <div class="logo col-lg-3 text-center text-lg-left">
                    <a class="d-block" href="index.html">
                      <img loading="lazy" :src="logoPath" style="width:180px; height:100px" alt="Constra"/>
                    </a>
                </div><!-- logo end -->
      
                <div class="col-lg-9 header-right">
                    <ul class="top-info-box">
                      <li>
                        <div class="info-box">
                          <div class="info-box-content">
                              <p class="info-box-title">Call Us</p>
                              <p class="info-box-subtitle">(+9) 847-291-4353</p>
                          </div>
                        </div>
                      </li>
                      <li>
                        <div class="info-box">
                          <div class="info-box-content">
                              <p class="info-box-title">Email Us</p>
                              <p class="info-box-subtitle">office@Constra.com</p>
                          </div>
                        </div>
                      </li>
                      <li class="last">
                        <div class="info-box last">
                          <div class="info-box-content">
                              <p class="info-box-title">Global Certificate</p>
                              <p class="info-box-subtitle">ISO 9001:2017</p>=
                          </div>
                        </div>
                      </li>
                      
                    </ul><!-- Ul end -->
                </div><!-- header right end -->
              </div><!-- logo area end -->
      
          </div><!-- Row end -->
        </div><!-- Container end -->
      </div>
    
      <div class="site-navigation">
        <div class="container">
            <div class="row">
              <div class="col-lg-12">
                  <nav class="navbar navbar-expand-lg navbar-dark p-0">
                    <button class="navbar-toggler" type="button" data-toggle="collapse" data-target=".navbar-collapse" aria-controls="navbar-collapse" aria-expanded="false" aria-label="Toggle navigation">
                        <span class="navbar-toggler-icon"></span>
                    </button>
                    
                    <div id="navbar-collapse" class="collapse navbar-collapse">
                        <ul class="nav navbar-nav mr-auto">
                          <li :class="{active: isActive('/')}"><router-link :to="{name:'home'}" class="nav-link">Beranda</router-link></li>
                          <li :class="{active: isActive('/post')}"><router-link :to="{name:'post'}" class="nav-link">Berita</router-link></li>
                          <li class="nav-item">
                              <a href="#" class="nav-link dropdown-toggle" data-toggle="dropdown">About Us <i class="fa fa-angle-down"></i></a>
                              <ul class="dropdown-menu" role="menu">
                                <li class=""><a href="index.html">Struktur Organisasi</a></li>
                                <li><a href="index-2.html">Visi dan Misi</a></li>
                                <li><a href="index-2.html">Profile</a></li>
                              </ul>
                          </li>
                          <li :class="{active: isActive('/photo')}"><router-link :to="{name:'photo'}" class="nav-link">Galeri</router-link></li>
                          <li :class="{active: isActive('/video')}"><router-link :to="{name:'video'}" class="nav-link">Video</router-link></li>
                          <li class="nav-item dropdown" :class="{active: isActive('/event')}">
                              <a href="#" class="nav-link dropdown-toggle" data-toggle="dropdown">Publik <i class="fa fa-angle-down"></i></a>
                              <ul class="dropdown-menu" role="menu">
                                <li><router-link :to="{name: 'event'}" >Event</router-link></li>
                              </ul>
                          </li>
                  
                          <li class="nav-item"><router-link :to="{name: 'contact'}" class="nav-link">Contact</router-link></li>
                        </ul>
                    </div>
                  </nav>
              </div>
              <!--/ Col end -->
            </div>
            <!--/ Row end -->
    
            <div class="nav-search">
              <span id="search"><i class="fa fa-search"></i></span>
            </div><!-- Search end -->
    
            <div class="search-block" style="display: none;">
              <label for="search-field" class="w-100 mb-0">
                <input type="text" class="form-control" id="search-field" placeholder="Type what you want and enter">
              </label>
              <span class="search-close">&times;</span>
            </div><!-- Site search end -->
        </div>
        <!--/ Container end -->
    
      </div>
      <!--/ Navigation end -->
    </header>
</template>

<script>

export default {
    name: 'HeaderComponent',
    methods: {
    isActive(route) {
      return this.$route.path === route;
    },
  },
    computed: {
    logoPath() {
      return new URL(`/assets/images/logo.jpg`, import.meta.url).href;
    }
  }
};
</script>