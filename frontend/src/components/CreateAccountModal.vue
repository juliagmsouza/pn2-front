<template>
    <div>
        <b-row class="pt-1 px-2">
            <label for="name-input" style="margin-left: -6px">Nome Completo*:</label>
            <b-form-input id="name-input" v-model="nameInput">
            </b-form-input>
        </b-row>
        <b-row class="pt-1 px-2">
            <label for="email-input" style="margin-left: -6px">Email*:</label>
            <b-form-input id="email-input" v-model="emailInput">
            </b-form-input>
        </b-row>
        <b-row class="pt-1 px-2">
            <label for="password-input" style="margin-left: -6px">Senha*:</label>
            <b-form-input id="password-input" v-model="passwordInput">
            </b-form-input>
        </b-row>
        <hr style="width: 107%; margin-left: -16px">
        <b-row align-h="end">
            <b-col class="justify-content-end d-flex" cols="7" style="padding-right: 0">
                <b-button @click="closeModal" variant="secondary">
                    Cancelar
                </b-button>
                <b-button style="margin-left: 4%; margin-right: 3%" variant="primary" :disabled="nameInput.length === 0 || emailInput.length === 0 || passwordInput.length === 0">  
                    Criar conta
                </b-button>
            </b-col>
        </b-row>
    </div>
</template>

<script>
export default {
    data() {
        return {
            nameInput: '',
            emailInput: '',
            passwordInput: ''
        }
    },
    methods: {
        closeModal() {
            this.$bvModal.hide('create-account-modal')
        }
    }
}
</script>