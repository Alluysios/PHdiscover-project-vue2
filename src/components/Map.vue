<template>
    <div id="container">
        <div class="form-container"> 
            <Form v-bind:show="show" v-on:closeForm="close" v-on:trail="addTrail" />
        </div>
        <div id="mapContainer"></div>
    </div>
</template>

<script>
    import "leaflet/dist/leaflet.css";
    import L from "leaflet";
    import Form from './Form.vue';

    export default {
        name: "Map",
        data() {
            return{
                show: false,
                trail: null,
                map: null,
                mapIcon: null
            }
        },
        watch: {
            markerPosition: function(val) {
                this.map.setView([val[0], val[1]], 15);
            }
        },
        props: ['trails', 'markerPosition'],
        components: {
            Form
        },
        methods: {
            close(show) {
                this.show = show;
            },
            setupLeafletMap: function () {
                this.map = L.map('mapContainer', { closePopupOnClick: false }).setView([10.309008, 123.918636], 12);
                L.tileLayer(
                "https://api.mapbox.com/styles/v1/{id}/tiles/{z}/{x}/{y}?access_token={accessToken}",
                {
                    attribution: 'Map data &copy; <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors, <a href="https://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, Imagery © <a href="https://www.mapbox.com/">Mapbox</a>',
                    maxZoom: 18,
                    id: 'mapbox/streets-v11',
                    tileSize: 512,
                    zoomOffset: -1,
                    accessToken: 'pk.eyJ1IjoiYWxsdXlzaW9zIiwiYSI6ImNrOWo1amthMzA1a2kzcG80ajN0cDg5bm4ifQ.udO-buen_3AHbGLtRNopYA'
                }).addTo(this.map);
                this.mapIcon = L.icon({
                    iconUrl: require('@/assets/Images/placeholder.png'),
                    iconSize:     [35, 35], // size of the icon
                    iconAnchor:   [18, 45], // point of the icon which will correspond to marker's location
                    popupAnchor:  [0, -45] // point from which the popup should open relative to the iconAnchor
                });
                this.map.on('click', (e) => this.showForm(e));
            },
            showForm(e) {
                this.show = true;
                this.trail = {
                    latlng: [e.latlng.lat, e.latlng.lng]
                }
            },
            addTrail(formData) {
                this.show = false;
                this.trail = { ...this.trail, ...formData}
                this.$emit('newTrail', this.trail);
                this.addMarker();
            },
            addMarker() {
                const marker = L.marker([this.trail.latlng[0], this.trail.latlng[1]], { icon: this.mapIcon }).addTo(this.map);
                marker.bindPopup(this.trail.name, { autoClose: false, autoPan: false }).openPopup();
            },  
            setMarkers() {
                for(var i = 0; i < this.trail.length; i++) {
                    const mark = L.marker([this.trail[i].latlng[0], this.trail[i].latlng[1]], { icon: this.mapIcon}).addTo(this.map);
                    mark.bindPopup(this.trail[i].name, { autoClose: false }).openPopup();
                }
            }
        },
        computed: {

        },
        created() {
            this.trail = this.trails;
        },
        mounted() {
            this.setupLeafletMap();
            this.setMarkers();
        },
    };
</script>

<style scoped>
#container {
    height: 100%;
    position: relative;
    top: 0;
    left: 0;
}
.form-container {
    position: absolute;
    width: 100%;
    top: 1rem;
    z-index: 99999;
}
#mapContainer {
    height: 100%;
    width: 100%;
}
</style>