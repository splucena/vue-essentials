<template>
    <transition name="custom" enter-active-class="animated fadeInDown" leave-active-class="animated slideOutRight">
        <div v-if="sliderStatus">
            <div :class="sliderState">
                <div class="form-group">                    
                    <label for="maximum" class="form-group-label">Maximum</label>
                    <input type="text" class="form-control" v-model="maxAmount" @change="$parent.$emit('update:maximum', maxAmount)" id="maximum">
                    <label for="maxRange" class="form-group-label">Range</label>
                    <input type="range" id="maxRange" v-model="maxAmount" @input="$parent.$emit('update:maximum', maxAmount)" class="custom-range" min="0" max="1000">
                </div>
            </div>
        </div>
    </transition>
</template>

<script>
export default {
    name: "price-slider",
    data: function() {
        return {
            maxAmount: 99,
        }
    },
    props: ['sliderStatus'],
    computed: {
        sliderState: function () {
            return this.sliderStatus ? 'd-flex' : 'd-none';
        },
    }
}
</script>

<style scoped>

</style>