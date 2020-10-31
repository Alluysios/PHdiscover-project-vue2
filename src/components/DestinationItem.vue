<template>
    <div id='destinationitem' class='item'>
        <span class="item-name">
            Name: {{ trail.name }}
        </span>
        <span class="item-island">
            Island: {{ trail.island }}
        </span>
        <span class="item-type">
            Type: {{ trail.type }}
        </span>
        <span class="item-popularity">
            popularity: {{ trail.popular }}
        </span>
        <button class="item-button" v-on:click="viewMapMarker">
            CHECK!
        </button>
    </div>
</template>

<script>
    export default {
        name: 'DestinationItem',
        props: ['trail'],
        methods: {
            viewMapMarker() {
                this.$emit('latlng', this.trail.latlng)
            }
        }
    }
</script>

<style scoped>
    .item {
        width: 95%;
        background: rgb(235, 232, 232);
        margin: 0 auto;
        padding: 1rem;
        margin-top: 10px;
        color: #333;
        font-size: 18px;
    }
    .item > span {
        display: inline-block;
        width: 100%;
        padding: 3px 0;
    } 
</style>