<template>
  <nav>
    <v-navigation-drawer v-model="drawer" dark app class="grey darken-3 py-0">
      <v-container>
        <v-row>
          <v-col md="9">
            <v-progress-circular
              :rotate="300"
              :size="50"
              :width="7"
              :value="value"
              color="lime accent-3"
              class="mt-n1"
              >{{ value }}
            </v-progress-circular>
          </v-col>
          <v-col md="3">
            <v-icon class="mt-1" right>fas fa-bars</v-icon>
          </v-col>
        </v-row>
      </v-container>
      <v-list nav dense>
        <v-list-item
          v-for="navItem in navItems"
          :key="navItem.name"
          :to="`/${navItem.path}`"
          router
        >
          <v-list-item-action>
            <v-icon small>{{ navItem.icon }}</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title>{{ navItem.name }}</v-list-item-title>
          </v-list-item-content>
          <v-chip
            v-if="navItem.name === 'Applicants'"
            color="yellow darken-3"
            small
            >3
          </v-chip>
        </v-list-item>
      </v-list>
      <v-layout row style="position: absolute; bottom: 0; width: 100%">
        <v-flex md-10 class="mb-3">
          <v-list-item dense>
            <v-list-item-avatar class="ml-2">
              <v-img src="woman.png"></v-img>
            </v-list-item-avatar>
            <v-list-item-action class="ml-8">
              <v-badge color="error" overlap>
                <template slot="badge"> 3 </template>
                <v-icon color="tertiary">mdi-bell</v-icon>
              </v-badge>
            </v-list-item-action>
          </v-list-item>
        </v-flex>
        <v-flex md-2>
          <v-tooltip top>
            <template v-slot:activator="{ on }">
              <v-btn text icon v-on="on" class="mt-2">
                <v-icon dark right>fas fa-sign-out-alt</v-icon>
              </v-btn>
            </template>
            <span>Exit</span>
          </v-tooltip>
        </v-flex>
      </v-layout>
    </v-navigation-drawer>
  </nav>
</template>

<script>
export default {
  name: "NavBar",

  data: () => ({
    drawer: true,
    interval: {},
    value: 0,

    navItems: [
      { icon: "fas fa-tachometer-alt", name: "Dashboard", path: "" },
      { icon: "fas fa-users", name: "Applicants", path: "applicantsview" },
      { icon: "fas fa-briefcase", name: "Jobs", path: "jobs" },
      { icon: "fas fa-calendar-alt", name: "Calender", path: "calender" },
      { icon: "fas fa-clipboard-list", name: "Reports", path: "reports" },
    ],
  }),
  beforeDestroy() {
    clearInterval(this.interval);
  },

  mounted() {
    this.interval = setInterval(() => {
      if (this.value === 100) {
        return (this.value = 0);
      }
      this.value += 10;
    }, 1000);
  },
};
</script>

<style scoped>
.v-progress-circular {
  margin: 1rem;
}
</style>
