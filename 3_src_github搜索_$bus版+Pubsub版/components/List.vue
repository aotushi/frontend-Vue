<template>
    <div class="row">
        <h2 v-show='listInfo.isFirst'>欢迎使用</h2>
        <h2 v-show='listInfo.isLoading'>Loading</h2>
        <h2 v-show='listInfo.errMsg'>{{listInfo.errMsg}}</h2>
        <div v-show='listInfo.users.length' class="card" v-for="user in listInfo.users" :key="user.id">
            <a :href="user.html_url" target="_blank">
                <img :src="user.avatar_url" style="width: 100px" />
            </a>
            <p class="card-text">{{user.login}}</p>
        </div>
    </div>
</template>

<script>
import Pubsub from 'pubsub-js';
export default {
    name: "List",
    data() {
        return {
            listInfo: {
                users: [],
                isFirst: true,
                isLoading: false,
                errMsg: "",
            },
        };
    },
    methods: {
        saveData(_, data) {
            this.listInfo={...this.listInfo, ...data}
        },
    },
    mounted() {
        //this.$bus.$on("get-list-data", this.saveData);
        Pubsub.subscribe('get-list-data', this.saveData)
    },
};
</script>

<style>
.album {
    min-height: 50rem; /* Can be removed; just added for demo purposes */
    padding-top: 3rem;
    padding-bottom: 3rem;
    background-color: #f7f7f7;
}

.card {
    float: left;
    width: 33.333%;
    padding: 0.75rem;
    margin-bottom: 2rem;
    border: 1px solid #efefef;
    text-align: center;
}

.card > img {
    margin-bottom: 0.75rem;
    border-radius: 100px;
}

.card-text {
    font-size: 85%;
}
</style>
