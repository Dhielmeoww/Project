<template>
  <q-page class="tw-flex tw-justify-center">
    <div class="q-pa-md">
      <q-form @submit="onSubmit" @reset="onReset" class="q-gutter-md">
        <h1 class="tw-my-7 tw-text-xl tw-text-center">Welcome to My Web</h1>
        <q-input
          filled
          v-model="username"
          label="Username *"
          hint="Username"
          lazy-rules
          class="tw-w-[600px]"
        />

        <q-input
          filled
          type="password"
          v-model="password"
          label="Password *"
          lazy-rules
          class="tw-w-[600px]"
        />

        <vue-recaptcha
          ref="recaptcha"
          sitekey="6LeWJlgnAAAAANqoSWB3VRn1APW8b2pwfglCgci9"
        >
        </vue-recaptcha>

        <div>
          <q-btn label="Submit" type="submit" color="primary" />
        </div>
      </q-form>
    </div>
  </q-page>
</template>

<script>
import { defineComponent, ref } from "vue";
import { VueRecaptcha } from "vue-recaptcha";

export default defineComponent({
  name: "IndexPage",
  components: {
    VueRecaptcha,
  },
  setup() {
    return {
      username: ref(""),
      password: ref(""),
    };
  },
});
</script>
