<template>
    <div id="add-blog">
        <h2>Add a new blog post</h2>
        <form v-show="!submitted">
            <label>Blog Title: </label>
            <input type="text" required v-model.lazy="blog.title">
            <label>Blog Content: </label>
            <textarea v-model.lazy="blog.content"></textarea>
            <div id="checkboxes">
                <label>World</label>
                <input type="checkbox" value="world" v-model="blog.categories">
                <label>Asia</label>
                <input type="checkbox" value="asia" v-model="blog.categories">
                <label>Europe</label>
                <input type="checkbox" value="europe" v-model="blog.categories">
                <label>Africa</label>
                <input type="checkbox" value="africa" v-model="blog.categories">
            </div>
            <label>Author:</label>
            <select v-model="blog.author">
                <option v-for="author in authors">{{ author }}</option>
            </select>
            <button v-on:click.prevent="post">Add blog</button>
        </form>
        <div v-if="submitted">
            <h3>Thanks for adding post</h3>
        </div>
        <div id="preview">

            <h3>Preview Blog</h3>
            <p>Blog Title: </p>
            <p>{{ blog.title }}</p>
            <p>Blog Content: </p>
            <p>{{ blog.content }}</p>
            <p>Blog Categories: </p>
            <ul>
                <li v-for="category in blog.categories">{{ category }}</li>
            </ul>
            <p>Author: {{ blog.author }}</p>
        </div>
    </div>
</template>

<script>
    export default {
        data () {
            return {
                blog: {
                    title: '',
                    content: '',
                    categories: [],
                    author: ''
                },
                authors: ['Sherlock','Microft','John'],
                submitted: false
            }
        },
        methods: {
            post: function () {
                this.$http.post('http://jsonplaceholder.typicode.com/posts', {
                    title: this.blog.title,
                    content: this.blog.content,
                    author: this.blog.author,
                    categories: this.blog.categories
                }).then(function (data) {
                    console.log(data);
                    this.submitted = true
                });
            }
        }
    }
</script>

<style>
    #add-blog *{
        box-sizing: border-box;
    }
    #add-blog{
        margin: 20px auto;
        max-width: 500px;
    }
    label{
        display: block;
        margin: 20px 0 10px;
    }
    input[type="text"], textarea{
        display: block;
        width: 100%;
        padding: 8px;
    }
    #preview{
        padding: 10px 20px;
        border: 1px dotted #ccc;
        margin: 30px 0;
    }
    h3{
        margin-top: 10px;
    }

    #checkboxes input {
        display: inline-block;
        margin-right: 10px;
    }

    #checkboxes label {
        display: inline-block;
    }
</style>
