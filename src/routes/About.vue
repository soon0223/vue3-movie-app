<template>
    <div class="about">
        <div class="photo">
            <Loader 
                v-if="imageLoading"
                absolute/>
            <img 
                :src="image" 
                alt="name">
        </div>
        <div class="name">
            {{name}}
        </div>
        <div>{{github}}</div>
    </div>
</template>


<script>
import {mapState} from 'vuex'
import Loader from '../components/Loader'
export default {
    data() {
        return {
            imageLoading: true
        };
    },
    computed: {
        ...mapState('about', [
            'image',
            'name',
            'github',
        ])
    },
    mounted() {
        this.init();
    },
    methods: {
        async init() {
            await this.$loadImage(this.image);
            this.imageLoading = false;
        }
    },
    components: { Loader }
}
</script>


<style lang="scss" scoped>
.about {
    text-align: center;
    .photo {
        position: relative;
        width: 250px;
        height: 250px;
        margin: 40px auto 20px;
        border: 7px solid $primary;
        border-radius: 50%;
        box-sizing: border-box;
        background-color: $gray-200;
        img {
            width: 100%;
        }
    }
    .name {
        font-size: 40px;
        font-family: "Oswald", serif;
        margin-bottom: 20px;
    }
}
</style>