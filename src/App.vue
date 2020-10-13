<template>
  <v-app>
    <v-content>
      <!-- Es como el CONTAINER de bootstrap.  -->
      <v-container>
        <router-view/>
        <div class="text-center">
          <v-dialog v-model="loading.estado" hide-overlay persistent width="300">
            <v-card color="success" dark>
              <v-card-text>Please stand by
                <v-progress-linear indeterminate color="white" class="mb-0">{{loading.titulo}}</v-progress-linear>
              </v-card-text>
            </v-card>
          </v-dialog>
        </div>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
import { mapState } from "vuex";
export default {
  name: 'App',

  components: {
  },

  data: () => ({
    //
  }),
  computed: {
    ...mapState(['loading'])
  }
};
</script>
