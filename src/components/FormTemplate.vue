<template>
  <v-container>
    <v-card
      class="mx-auto"
      max-width="500"
    >
      <v-card-title>Login</v-card-title>
      <v-card-text>
        <v-form @submit.prevent="handleSubmit">
          <v-text-field
            v-model.trim="state.email"
            class="my-1"
            :error-messages="v$.email.$errors.map(error => error.$message)"
            label="Email"
            variant="solo"
            type="email"
          />
          <v-text-field
            v-model.trim="state.password"
            class="my-1"
            :error-messages="v$.password.$errors.map(error => error.$message)"
            label="Password"
            variant="solo"
            type="password"
            autocomplete="on"
          />
          <v-card-actions>
            <v-spacer />
            <v-btn
              color="primary"
              type="submit"
              :disabled="v$.$invalid"
            >
              Login
            </v-btn>
          </v-card-actions>
        </v-form>
      </v-card-text>
    </v-card>
  </v-container>
</template>

<script>
import { defineComponent, reactive } from 'vue';
import { useRouter } from 'vue-router';
import { required, email, minLength } from '@vuelidate/validators';
import { useVuelidate } from '@vuelidate/core';

export default defineComponent({
  setup() {
    const router = useRouter();

    const state = reactive({
      email: '',
      password: '',
    })

    const rules = {
      email: {required, email},
      password: {required, minLength: minLength(6)}
    }

    const v$ = useVuelidate(rules, state, { $lazy: true });

    const handleSubmit = () => {
      v$.value.$touch()

      if (!v$.value.$error) {
        router.push('/game');
      }
    }

    return { state, v$, handleSubmit }
  }
});
</script>

