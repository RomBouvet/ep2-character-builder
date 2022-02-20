<template>
  <div>
    <q-img src="/auth_bg.jpg" cover/>

    <q-form
      @submit="onSubmit"
      style="min-width: 400px"
      class="q-pa-md absolute-center bg-grey-1"
    >
      <div class="text-h5">S'identifier</div>
      <q-input
        filled
        v-model="email"
        label="Email *"
        lazy-rules
        :rules="[ val => val && val.length > 0 || 'Must be a valid mail']"
      />

      <q-input
        filled
        type="password"
        v-model="password"
        label="Password *"
        lazy-rules
        :rules="[ val => val !== null && val !== '' || 'Please type something' ]"
      />

      <div>
        <q-btn label="Submit" type="submit" color="primary"/>
      </div>
    </q-form>
  </div>
</template>

<script>
import { defineComponent, ref } from 'vue';

export default defineComponent({
  name: 'PageIndex',
  setup() {
    return {
      email: ref(''),
      password: ref(''),
    };
  },
  methods: {
    onSubmit() {
      this.$api.post('/authentication', {
        email: 'bouvet.romain18@gmail.com',
        password: 'test',
        strategy: 'local',
      }).then((e) => {
        console.log('test');
        console.log(e);
        if (!this.$route.query.redirectTo) {
          console.log('no redirect');
          this.$router.push('/');
        } else {
          console.log('redirect');
          this.$router.push(this.$route.query.redirectTo);
        }
      });
    },
  },
});
</script>
