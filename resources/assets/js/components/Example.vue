<template>
    <div class="links">
        <a href="#">{{url}} http status code: <span v-html="code"></span></a>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                url: '/api/user',
                code: '000'
            }
        },
        mounted() {
            console.log('Component mounted.');
            this.getUser();
        },
        methods: {
            getUser() {
                let vm = this;
                window.axios.get(this.url, {
                    validateStatus: function (status) {
                        return status < 500; // Reject only if the status code is greater than or equal to 500
                    }
                })
                .then(function (response) {
                    vm.code = response.status;
                });
            }
        }
    }
</script>
