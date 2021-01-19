<template>
    <section class="jumbotron">
        <h3 class="jumbotron-heading">Search Github Users</h3>
        <div>
            <input
                type="text"
                placeholder="enter the name you search"
                v-model="word"
            />&nbsp;<button @click="getUserInfo">Search</button>
        </div>
    </section>
</template>

<script>
import axios from "axios";
export default {
    name: "Search",
    data() {
        return {
            word: "",
        };
    },
    methods: {
        async getUserInfo() {
            //请求之前通知List组件更新状态
            this.$bus.$emit('get-list-data',{isFirst:false, isLoading:true});
            try {
                const result = await axios.get(" https://api.github.com/search/users",{ params: { q: this.word } });
                const { items } = result.data;
                //请求成功后,通知List组件更新状态
                this.$bus.$emit('get-list-data', {isLoading:false, users:items});
                //this.$bus.$emit("get-data", items);
            } catch (error) {
                //请求失败后,通知List组件更新状态
                this.$bus.$emit('get-list-data', {isLoading:false, users:[], errMsg:error.message});

            }
        },
    },
};
</script>

<style></style>
