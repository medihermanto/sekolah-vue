<template>
<div id="myCarousel" class="carousel slide" data-ride="carousel">
        <ol class="carousel-indicators">
            <li data-target="#myCarousel" data-slide-to="0" class="active"></li>
            <li data-target="#myCarousel" data-slide-to="1"></li>
            <li data-target="#myCarousel" data-slide-to="2"></li>
        </ol>
        <div class="carousel-inner">
          <div v-if="sliders.length > 0">
            <div class="carousel-item" v-for="(slider, id) in sliders" :class="{ active: id==0 }" :key='slider.id' v-bind:style="{'background-image': 'url(' + slider.image +')'}">
              <img :src="slider.image"
                    class="w-100" style="height:700px;object-fit:cover" >
              
            </div>
          </div>
          <div v-else class="mt-5">
            <div class="card border-0 shadow-sm rounded-lg mb-3" v-for="loader in sliders_loader" :key="loader">
                    <div class="card-body pt-4">
                        <ContentLoader />
                    </div>
                </div>
          </div>
        </div>
        <a class="carousel-control-prev" href="#myCarousel" role="button" data-slide="prev">
            <span class="carousel-control-prev-icon" aria-hidden="true"></span>
            <span class="sr-only">Previous</span>
        </a>
        <a class="carousel-control-next" href="#myCarousel" role="button" data-slide="next">
            <span class="carousel-control-next-icon" aria-hidden="true"></span>
            <span class="sr-only">Next</span>
        </a>
    </div>
</template>

<script>
import {
    ContentLoader
} from 'vue-content-loader';

import axios from 'axios';

import {ref, onMounted} from 'vue';

export default {
    name : 'SliderComponent',

    components: {
        ContentLoader
    },
    

    setup() {
        const sliders = ref([]);

        const sliders_loader = ref(1);

        onMounted(() => {
            axios.get('/api/slider')
            .then(response => {
                sliders.value = response.data.data.data;
            })
            .catch(() => {
                sliders.value = [];
            });
        });

        return {
            sliders,
            sliders_loader
        }
    }
}
</script>