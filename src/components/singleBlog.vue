<template>
    <div id="single-blog">
        <h1>{{ body.title }}</h1>
        <article>{{ body.body }}</article>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                id: this.$route.params.id,
                body: {}
            }
        },
        created() {
            this.$http.get('http://jsonplaceholder.typicode.com/posts/' + this.id).then(function (data) {
               this.body = data.body
            });
        }
    }
</script>

<style scoped>
    #single-blog {
        max-width: 960px;
        margin: 0 auto;
    }
</style>