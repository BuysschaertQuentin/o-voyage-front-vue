<script setup lang="ts">
import inputWidget from '@/components/widgets/inputWidget.vue'
import ContainerFormWidget from '@/components/widgets/ContainerFormWidget.vue'
import { useAuthStore } from '@/stores/auth.store'
import { useRouter } from 'vue-router'
import { ref } from 'vue'
import { useAlertStore } from '@/stores/alert.store'

const authStore = useAuthStore()
const alertStore = useAlertStore()
const router = useRouter()
const forms = ref([
  {
    name: 'email',
    label: 'Email',
    type: 'email',
    value: '',
    placeholder: 'Entrez votre email',
    required: true,
    disabled: false,
    autocomplete: 'email',
    isPassword: false
  },
  {
    name: 'password',
    label: 'Mot de passe',
    type: 'password',
    value: '',
    placeholder: 'Entrez votre mot de passe',
    required: true,
    disabled: false,
    autocomplete: 'current-password',
    isPassword: true
  }
])

async function submitForm(event: Event) {
  event.preventDefault()
  const email = forms.value[0].value
  const password = forms.value[1].value
  const res = await authStore.signIn({ email, password })
  if (res) {
    alertStore.showAlert({
      message: 'Vous êtes connecté',
      type: 'info'
    })
    router.push({ name: 'Home' })
  }
}
</script>

<template>
  <ContainerFormWidget title="Connexion">
    <form @submit="submitForm" class="flex flex-col gap-4">
      <inputWidget
        v-for="form in forms"
        :key="form.label"
        v-model="form.value"
        :name="form.name"
        :label="form.label"
        :type="form.type"
        :placeholder="form.placeholder"
        :required="form.required"
        :disabled="form.disabled"
        :autocomplete="form.autocomplete"
        :isPassword="form.isPassword"
      />
      <div class="flex flex-col items-center">
        <button
          type="submit"
          class="btn btn-primary w-full"
          :disabled="forms[0].value === '' || forms[1].value === ''"
        >
          Se connecter
        </button>
      </div>
    </form>
  </ContainerFormWidget>
</template>