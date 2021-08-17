<template>
    <div id="app">
        <full-page :options="options" id="fullpage" v-if="isLoaded">
            <div
                v-for="soccerNew in soccerNews"
                :key="soccerNew.data.id"
                class="section"
            >
                <div class="container">
                    <img :src="'/img/soccer.png'" alt="shower icon" />
                    <div class="quote-symbol">“</div>
                    <p class="quote">
                        <a :href="soccerNew.data.url">{{
                            soccerNew.data.title
                        }}</a>
                    </p>
                    <div class="details">
                        <div class="details-authoor">
                            Author: {{ soccerNew.data.author }}
                        </div>
                        <div class="stats">
                            {{ soccerNew.data.ups }} Upvote |
                            {{ soccerNew.data.num_comments }} Comments
                        </div>
                    </div>
                </div>
            </div>
        </full-page>
        <div v-else>
            <loading-spinner />
        </div>
    </div>
</template>

<script>
import LoadingSpinner from "./LoadingSpinner.vue";

export default {
    name: "App",
    components: {
        LoadingSpinner
    },
    created() {
        fetch("https://www.reddit.com/r/soccer.json?limit=20")
            .then(response => response.json())
            .then(data => {
                this.soccerNews = data.data.children;
                this.soccerNews.shift();
                this.soccerNews.shift();
                this.isLoaded = true;
            });
    },
    data() {
        return {
            isLoaded: false,
            soccerNews: [],
            options: {
                scrollBar: true,
                sectionsColor: [
                    "#41b883",
                    "#ff5f45",
                    "#0798ec",
                    "#fec401",
                    "#1bcee6",
                    "#ee1a59",
                    "#ba5be9",
                    "#b4b8ab",
                    "#41b883",
                    "#ff5f45",
                    "#0798ec",
                    "#fec401",
                    "#1bcee6",
                    "#ee1a59",
                    "#ba5be9",
                    "#b4b8ab",
                    "#41b883",
                    "#ff5f45",
                    "#0798ec",
                    "#fec401"
                ]
            }
        };
    }
};
</script>

<style>
@import url("https://fonts.googleapis.com/css?family=Sriracha&display=swap");

#app {
    font-family: sans-serif;
    color: #2d3748;
}

body {
    margin: 0;
    padding: 0;
}

h3 {
    margin: 0;
}

.container {
    margin: auto;
    max-width: 800px;
    padding: 80px 16px;
}

.section {
    text-align: center;
}

.quote-symbol {
    font-size: 64px;
    line-height: 0;
    margin-top: 50px;
    color: white;
}

.quote a {
    text-decoration: none;
    font-family: "Sriracha", cursive;
    color: white;
    font-size: 32px;
    line-height: 1.5;
}

.quote a:hover {
    color: #edf2f7;
}

.details-stats {
    margin-top: 4px;
}
</style>
