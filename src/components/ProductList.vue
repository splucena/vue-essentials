<template>
    <!-- JS -->
    <transition-group name="custom" tag="div" @beforeEnter="beforeEnter" @enter="enter" @leave="leave">
        <!-- animate.js -->
        <!--<transition-group name="custom" enter-active-class="animated fadeInRight"
        leave-active-class="animated slideOutRight">-->
        <div :class="rowArray" v-for="(d, index) in products" v-if="d.price <= Number(maximum)" :key="d.id"
            :data-index="index">
            <div class="col-2">
                <button class="btn btn-info" @click="$parent.$emit('add', d)">+</button>
            </div>
            <div class="col-4">
                <img class="img-fluid" :src="d.image" :alt="d.name">
            </div>
            <div class="col-6">
                <div class="card rounded-0">
                    <div class="card-header bg-primary text-light h6 rounded-0">{{ d.name }}</div>
                    <div class="card-body">
                        <p class="card-text">{{ d.description }}</p>
                    </div>
                    <div class="h6 card-footer text-danger d-flex justify-content-end">
                        <!-- price component with array props -->
                        <!--<price :value="d.price" :prefix="'&euro;'" :precision="2" :conversion=".87"></price>-->
                        <price :value="Number(d.price)"></price>
                    </div>
                </div>
            </div>
        </div>
    </transition-group>
</template>

<script>

import Price from './Price.vue';

export default {
    name: 'product-list',
    data: function() {
        return {
            rowArray: ['row', 'd-flex', 'align-items-center', 'mb-3']
        }
    },
    components: { Price },
    props: ['products', 'maximum'],
    methods: {
        beforeEnter: function (el) {
                el.className = 'd-none';
            },
            enter: function (el) {
                let delay = el.dataset.index * 100;
                setTimeout(function () {
                    el.className = 'row d-flex mb-3 align-items-center animated fadeInRight';
                }, delay);
            },
            leave: function (el) {
                let delay = el.dataset.index * 100;
                setTimeout(function () {
                    el.className = 'row d-flex mb-3 align-items-center animated fadeOutRight';
                }, delay);
            }
    }
}
</script>

<style scoped>

</style>