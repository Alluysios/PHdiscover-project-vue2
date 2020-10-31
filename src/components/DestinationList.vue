<template>
    <div id="destination">
        <DestinationItem v-on:latlng="viewMapMarker" v-bind:key="trail.id" v-bind:trail="trail" v-for="trail in trails" />
    </div>
</template>

<script>
    import DestinationItem from './DestinationItem.vue'

    export default {
        name: 'DestinationList',
        props:['trails'],
        components: { 
            DestinationItem
        },
        methods: {
            viewMapMarker(latlng) {
                this.$emit('latlng', latlng)
            }
        }
    }
</script>

<style scoped>
    #destination {
        height: 90vh;
        overflow-y: scroll;
    }
    @media only screen and (max-width: 700px) {
        #destination {
            height: 20vh;
        }
    }
    h1 {
        color: #FFFFFF;
    }
</style>