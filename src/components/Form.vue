<template>
    <form v-if="show" @submit="submitTrail" class="form">
        <span class='close' @click="closeForm">CLOSE</span>
        <div class="form__group">
            <label for="name">Trail Name</label>
            <input type="text" name="name" v-model="name" placeholder="bike trail" required>
        </div>
         <div class="form__group">
            <label for="island">Island</label>
            <input type="text" name="island" v-model="island" placeholder="Luzon, Visayas, Mindanao">
        </div>
        <div class="form__group">
            <label for="type">Type</label>
            <input type="text" name="type" v-model="type" placeholder="Trail, Restaurant, Sightseeing">
        </div>
        <div class="form__group">
            <label for="popular">Popularity</label>
            <input type="text" name="popular" v-model="popular" placeholder="not so, very, extreme">
        </div>
        <input type="submit" value="save" class="button" />
    </form>
</template>

<script>
    export default {
        name: 'Form',
        props: ['show'],
        data() {
            return {
                name: '',
                island: '',
                type: '',
                popular: ''
            }
        },
        methods: {
            closeForm() {
                this.$emit('closeForm', false);
            },
            submitTrail(e) {
                e.preventDefault();

                const trail = {
                    name: this.name,
                    island: this.distance,
                    type: this.time,
                    popular: this.difficulty
                }
                
                this.$emit('trail', trail)
            }
        }
    }
</script>

<style scoped>
    .close {
        text-align: right;
        width: 100%;
        color: #ffffff;
        cursor: pointer;
    }
    .form {
        position: relative;
        display: flex;
        flex-wrap: wrap;
        padding: 1rem;
        background: #333;
        width: 95%;
        border-radius: 6px;
        margin: 0 auto;
    }
    .form__group {
        flex: 1 0 48%;
        margin: 1%;
    }
    .form__group > label {
        font-size: 20px;
        display: inline-block;
        color: #ffffff;
        width: 100%;
    }
    .form__group > input {
        outline: none;
        border-radius: 3px;
        font-size: 16px;
        padding: 10px 10px;
        width: 100%;
    }
    .button {
        width: 100%;
        display: inline-block;
        margin-top: 10px;
        padding: 10px 18px;
        font-size: 18px;
        background-color: rgb(113, 90, 242);
        color: #FFF;
        border: none;
        border-radius: 6px;
    }

    
</style>