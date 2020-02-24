<template>
    <div class="message">
        <div class="message-header">
            Push to Stream .....
        </div>

        <div class="message-body">

            <form @submit.prevent="onSubmit" @keydown="form.errors.clear()">
                <p class="control">
                    <textarea class="textarea" v-model="form.body" cols="30" rows="10" placeholder="I have something to say ....."></textarea>
                    <span class="help is-danger" v-if="form.errors.has('body')" v-text="form.errors.get('body')"></span>
                </p>

                <p class="control">
                    <button class="button is-primary" :disabled="form.errors.any()" style="margin-top: 10px;">Submit</button>
                </p>

            </form>
        </div>

    </div>



</template>

<script>

    export default {
        name: "AddToStream",

        data() {
            return {
                form: new Form({
                    body: '',
                })
            }
        },

        methods: {
            onSubmit() {
                // submit an ajax request to the server

                this.form.post('/statuses')
                    .then(status => this.$emit('completed', status));


            }
        }

    }
</script>

<style scoped>

</style>
