<template>
    <div id="poke-list">
        <div class="card">
            <div class="card-image">
                <figure>
                    <img :src="currentImg">
                </figure>
            </div>
            <div class="card-content">
                <div class="media">
                    <div class="media-content">
                        <p class="title is-4">{{num}} - {{name | upperFirstLetter }}</p>
                        <p class="subtitle is-6">{{ pokemon.type }}</p>
                    </div>
                    </div>
                     <div class="content">
                         <button class="button is-medium is-fullwidth btn-changeSprite" @click="mudaSprite">Mudar Sprite</button>
                    </div>
                </div>
            </div>
    </div>
</template>

<script>

import axios from 'axios'; 

export default {
    created: function() {
        axios.get(this.url).then(res => {
            this.pokemon.type = res.data.types[0].type.name;
            this.pokemon.front = res.data.sprites.front_default;
            this.pokemon.back = res.data.sprites.back_default;
            this.currentImg = this.pokemon.front;
        })
    },
    data() {
        return {
            isFront : true,
            currentImg : '',
            pokemon: {
                type : '',
                front : '',
                back: ''
            }
        }
    },
    props: {
        num: Number,
        name: String,
        url: String
    },
    filters: {
        upperFirstLetter: function(value) {
            let newName = value[0].toUpperCase() + value.slice(1);
            return newName;
        }
    },
    methods: {
        mudaSprite: function() {
            if(this.isFront) {
                this.isFront = false;
                this.currentImg = this.pokemon.back;
            } else {
                this.isFront = true;
                this.currentImg = this.pokemon.front;
            }
        }
    }
}
</script>

<style scoped>
    #poke-list {
        margin-top: 2%;
    }
    .btn-changeSprite {
        font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
        font-weight: 600;
    }

    .btn-changeSprite:hover {
        background-color: #ef5350;
        color: #fff;
    }
</style>