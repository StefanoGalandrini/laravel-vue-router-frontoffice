<script>
import axios from 'axios';

export default {
    data() {
        return {
            name: '',
            email: '',
            message: '',
            showSuccess: false,
            isSending: false,
            showError: false,
            errors: {},
            // TODO: mostrare gli errori per ciascun input
        };
    },
    methods: {
        sendLead() {
            this.isSending = true;
            this.showSuccess = false;
            this.showError = false;
            this.errors = {};
            axios
                .post("http://localhost:8000/api/leads", {
                    name: this.name,
                    email: this.email,
                    message: this.message,
                })
                .then(response => {
                    this.isSending = false;

                    if (response.data.success) {
                        this.showSuccess = true;
                        this.resetForm();
                    } else {
                        this.showError = true;
                        this.errors = response.data.errors;
                    }
                });
        },
        resetForm() {
            this.name = '';
            this.email = '';
            this.message = '';
        },
    },
};
</script>

<template>
    <div class="container_mail">
        <div class="contents">
            <div v-if="showSuccess" class="alert alert-success alert-dismissible fade show" role="alert">
                Messaggio inviato con successo
                <button type="button" class="btn-close" aria-label="Close" @click="showSuccess = false"></button>
            </div>

            <div v-if="showError" class="alert alert-danger alert-dismissible fade show" role="alert">
                Errore nell'invio del messaggio
                <button type="button" class="btn-close" aria-label="Close" @click="showError = false"></button>
            </div>

            <form @submit.prevent="sendLead" novalidate class="form">
                <div class="mb-3">
                    <label for="name" class="form-label text-light">Name</label>
                    <input type="text" class="form-control" :class="{ 'is-invalid': errors.name }" id="name" v-model="name" />
                    <div class="invalid-feedback">
                        <p v-for="errorMessage in errors.name" :key="errorMessage">
                            {{ errorMessage }}
                        </p>
                    </div>
                </div>

                <div class="mb-3">
                    <label for="email" class="form-label text-light">Email address</label>
                    <input type="email" class="form-control" :class="{ 'is-invalid': errors.email }" id="email" v-model="email" />
                    <div class="invalid-feedback">
                        <template v-for="errorMessage in errors.email" :key="errorMessage">
                            {{ errorMessage }}<br />
                        </template>
                    </div>
                </div>

                <div class="mb-3">
                    <label for="message" class="form-label text-light">Message</label>
                    <textarea class="form-control" :class="{ 'is-invalid': errors.message }" id="message" rows="5"
                        v-model="message"></textarea>
                    <div class="invalid-feedback">
                        <template v-for="errorMessage in errors.message" :key="errorMessage">
                            {{ errorMessage }}<br />
                        </template>
                    </div>
                </div>

                <button type="submit" class="btn button" :disabled="isSending">
                    Submit
                </button>
            </form>
        </div>
    </div>
</template>

<style lang="scss" scoped>
.button {
  padding: 10px 22px;
  border-radius: 6px;
  border: none;
  color: #fff;
  background-color: #7d2ae8;
}

.container_mail {
    display: grid;
    height: 100vh;
    width: 100vw;
    align-items: center;
    justify-content: center;
}
</style>