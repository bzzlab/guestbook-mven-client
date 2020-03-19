<template>
    <div id="create_post">
    <h1>Guestbook</h1>
        <p>Did you enjoy our restaurant? What can we improve? Tell us, please.</p>
        <h4>Recent entries</h4>

        <!-- Task-1: Add code here -->
        <div v-for="eintrag in eintraege">
            <div class="card" style="width: 25rem;">
                <div class="card-body">
                    <h5 class="card-title">{{ eintrag.titel }}</h5>
                    <h6 class="card-subtitle mb-2 text-muted">From {{ eintrag.autor }}</h6>
                    <p class="card-text">{{ eintrag.text }}</p>
                </div>
            </div>
            <div style="margin-bottom: 1rem"></div>
        </div>
        <!-- Task-End -->

        <!-- Task-2: Add code here -->
        <h4 style="margin-top: 2rem; margin-bottom: 1rem">Post an entry</h4>
        <form v-on:submit.prevent="addPost">
            <div class="form-group col-md-6">
                <div class="form-group">
                    <label for="autor">Name</label>
                    <input v-model="eintrag.autor" type="text" class="form-control" id="autor" placeholder="Name">
                </div>
                <div class="form-group">
                    <label for="email">Name</label>
                    <input v-model="eintrag.email" type="text" class="form-control" id="email" placeholder="Email">
                </div>
                <div class="form-group">
                    <label for="titel">Title</label>
                    <input v-model="eintrag.titel" type="text" class="form-control" id="titel" placeholder="Title">
                </div>
                <div class="form-group">
                    <label for="text">Text</label>
                    <textarea v-model="eintrag.text" class="form-control" id="text" rows="3"/>
                </div>
                <div class="form-group">
                    <button type="submit" class="btn btn-primary" data-toggle="modal"
                            data-target="#confirmBlogEntry">Create</button>
                </div>
            </div>
        </form>
        <!-- Task-End -->

        <div style="margin-bottom: 5rem"> {{ message }} </div>
    </div>
</template>

<script>
    import store from '../../store';
    import http from 'axios'
    const API_URL = store.state.apiUrl;
    export default {
        //Task-3: Add code here
        name: "GuestbookCreate",
        data: () => ({
            message: null,
            eintraege: null,
            eintrag: {
                titel: "",
                text: "",
                autor: "",
                email: "",
                datum: ""
            }
        }),
        //Task-End
        mounted() {
            /*  When this site is called then mounted-function will be automatically called.
                It makes a call to the server with the corresponding API
             */
            //later replace by http.get(this.$store.state.apiUrl) ...
            http.get(API_URL +'/api/blog')
                .then(response => (this.eintraege = response.data));
        },
        methods:{
            //Used methods in the form
            //Task-4: Add code here
            addPost(){
                fetch(API_URL +'/api/blog',
                    {
                        method: 'POST',
                        body: JSON.stringify(this.eintrag),
                        headers: {"content-type":"application/json"}
                    })
                    .then(res => res.json());
                this.proceed();
            },
            //Task-End
            proceed(){
                //redirect to oder list
                this.$router.push("/blog");
                this.message = 'Guestbook entry posted.';
                location.reload();
            }
        }
    }
</script>
