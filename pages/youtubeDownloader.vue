<template>
    <div class="text-center">
        <h1>Youtube downloader</h1>
        <div class="form">
            <b-input v-model="youtube_url" class="form-components" placeholder="Youtube url">
            </b-input>
            <b-form-select class="form-components" v-model="selected" :options="options"></b-form-select>
            <b-button class="form-components" @click.prevent="searchUrl" variant="outline-primary">SEARCH</b-button>
            <div v-if="status == 0" class="text-center">Search now</div>
            <div v-if="status == 2">
                <div class="p-1" v-if="fetchedAudios.length > 0">
                    <h4>Audios</h4>
                    <div class="d-inline-flex p-2" v-for="(item, index) in fetchedAudios" :key="index">
                        <a class="makeButton" :href="item.link"><i class="fa fa-download" aria-hidden="true"></i> {{item.audio_quality}}</a>
                    </div>
                </div>
                <div class="text-center" v-else>No Audios.</div>
                <div class="p-1" v-if="fetchedVideos.length > 0">
                    <h4>Videos</h4>
                    <div class="d-inline-flex p-2" v-for="(item, index) in fetchedVideos" :key="index">
                        <a class="makeButton" :href="item.link"><i class="fa fa-download" aria-hidden="true"></i> {{item.video_quality}}</a>
                    </div>
                </div>
                <div class="text-center" v-else>No Videos.</div>
            </div>
            <div class="text-center" v-if="status == 1">Searching</div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'YTDown',
    layout: 'main',
    data() {
        return {
            typeTimer: null,
            status: 0,
            youtube_url: null,
            selected: 'all',
            fetchedAudios: [],
            fetchedVideos: [],
            options: [
                {
                    text: 'All',
                    value: 'all'
                }, {
                    text: 'Audio',
                    value: 'audio'
                }, {
                    text: 'Video',
                    value: 'video'
                }
            ]
        }
    },
    methods: {
        async searchUrl() {
            try { 
                this.status = 1
                this.fetchedAudios = this.fetchedVideos = []
                // const url = `http://localhost:3006/api/get-data?yt_url=${this.youtube_url}&type=${this.selected}`
                const url = `https://ytd-api-dev.herokuapp.com/api/get-data?yt_url=${this.youtube_url}&type=${this.selected}`
                const resp = await this.$axios.get(url)
                console.log(resp);
                if (resp?.data?.data?.audio) {
                    this.fetchedAudios = resp.data.data.audio
                } 
                if (resp?.data?.data?.video) {
                    this.fetchedVideos = resp.data.data.video
                }
                this.status = 2
            } catch (error) {
                console.log(error);
            }
        }, 
        
    }
}
</script>

<style>
@import 'https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css';
.form {
    margin-left: 50%;
    transform: translateX(-50%);
    padding: 5%;
    width: 75%;
    border: 1px solid gray;
    border-radius: 20px;
    box-shadow: 4px 4px;
}

.form-components {
    margin-top: 10px;
    border-radius: 20px;
    box-shadow: 4px 4px;
}

.makeButton {
    margin-top: -10px;
    padding-left: 5px;
    padding-right: 5px;
    border: 1px solid gray;
    border-radius: 5px;
    box-shadow: 4px 4px;
}
</style>
