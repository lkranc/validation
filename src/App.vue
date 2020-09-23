<template>
    <div id="app">
        <pre>{{ user }}</pre>
        <form @submit="handleSubmit" class="app-form">
            <input-text
                label="Email"
                type="email"
                :value.sync="$v.user.email.$model"
                :error="$v.user.email.$error"
                placeholder="Enter your email address"
                @blur="$v.user.email.$touch()"
            />
            <!-- Możnaby zbić prop error i event blur do obiektu pod nazwą validation-state
                 i tam przekazać $v.user.email wtedy logikę erroru można zrobić w komponencie
                 co myslicie o takim wyjściu? -->
            <input-text
                label="Password"
                type="password"
                :value.sync="$v.user.password.$model"
                placeholder="Enter your password"
                @blur="$v.user.password.$touch()"
            />
            <app-button
                type="submit"
                :async-loader="submit.isLoading"
                :disabled="$v.user.$anyError"
                @click="handleSubmit"
            >
                Log in
            </app-button>
            <!--  Zwyczajny sync wyglądałby np. :value.sync="user.email"                                -->
            <!--  zapis $v. ... .$model / $error jest brzydki ale nie znalazłem jeszcze sposobu
                  na to żeby przekazać referencje do obiektu, może jakaś funkcja
                  która będzie mapować obiekt na jego kopie z $v
                  Jeśli ktoś ma jakiś pomysł, czy propozycje jakbyś chciał żeby to było rozwiązane
                  to śmiało piszcie -->
        </form>
        <pre>
            {{ $v }}
        </pre>
    </div>
</template>

<script>

import InputText from "@/components/form/InputText"
import AppButton from "@/components/form/AppButton"
import required from 'vuelidate/lib/validators/required'
import email from 'vuelidate/lib/validators/email'
import alphaNum from 'vuelidate/lib/validators/alphaNum'
// można zrobić: import { required, ... , } from 'vuelidate/lib/validators
// lub           import required from 'vuelidate/lib/validators/required'

export default {
    name: 'App',
    components: { AppButton, InputText },
    data: () => ({
        user: {
            email: '',
            password: '',
        },
        submit: {
            isLoading: false,
            isError: false,
        }
    }),
    validations: {
        user: {
            email: {
                required,
                email
            },
            password: {
                required,
                alphaNum
            }
        }
    },
    watch: {
        /** Gdybyśmy potrzebowali dodatkowy watch */
        'user.email'() {},
        'user.password'() {}
    },
    methods: {
        handleSubmit() {
            this.$v.$touch()
            this.submit.isLoading = true
            setTimeout(() => {
                this.submit.isLoading = false
            }, 2000)
        }
    },
    mounted() {
        this.$v.user.$touch()
    }
}
</script>

<style lang="scss">
#app {
    .app-form {}
}
</style>
