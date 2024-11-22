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
      <v-list nav>
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
      { icon: "fas fa-users", name: "Applicants", path: "applicants" },
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
