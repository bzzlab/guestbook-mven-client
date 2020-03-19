<template>
    <div id="create_post">
    <h1>Guestbook</h1>
        <p>Did you enjoy our restaurant? What can we improve? Tell us, please.</p>
        <h4>Recent entries</h4>

        <!-- Task-1: Add code here -->

        <!-- Task-End -->

        <!-- Task-2: Add code here -->

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
