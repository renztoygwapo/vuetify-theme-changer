<template>
  <v-layout>
    <v-flex xs12 sm12 md12 lg12 class="ml-3 mr-3 mb-3">
      <v-card>
        <v-toolbar color="primary">
          <v-toolbar-title class="white-text">Other Settings</v-toolbar-title>
          <v-spacer></v-spacer>
        </v-toolbar>
        <v-card-text>
          <v-layout row wrap>
            <v-flex xs12 md3>
              <v-subheader>
                Theme
              </v-subheader>
              <v-switch
                :label="switch1 ? 'Light' : 'Dark'" v-model="switch1">
              </v-switch>
            </v-flex>
            <v-flex xs12 md3>
              <v-subheader>
                Theming
              </v-subheader>
              <v-radio-group v-model="userTheme">
                <v-radio
                  v-for="themePreset in themePresets"
                  :key="themePreset.id"
                  :label="`${themePreset.name}`"
                  :value="themePreset.id - 1"
                ></v-radio>
              </v-radio-group>
            </v-flex>
          </v-layout>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="primary" @click="saveChanges">Save Changes</v-btn>
        </v-card-actions>
      </v-card>
    </v-flex>
  </v-layout>
</template>
<script>
module.exports = {
  methods: {
    saveChanges () {
      this.selectedConfigurations = {
        color: this.color[this.userTheme]
      }
      this.$emit('save', this.selectedConfigurations)
    }
  },
  data: function () {
    return {
      selectedConfigurations: {},
      switch1: true,
      userTheme: 0,
      color: [
        {
          primary: '#f44336',
          secondary: '#F50057',
          accent: '#008080',
          danger: '#d53182',
          error: '#b71c1c',
          info: '#1c89d5',
          clean: '#fff'
        },
        {
          primary: '#1c095E',
          secondary: '#914679',
          accent: '#E8BAB5',
          danger: '#d53182',
          error: '#EF5B8C',
          info: '#1c89d5',
          clean: '#fff'
        },
        { 
          primary: '#df691a',
          secondary: '#4e5d6c',
          accent: '#5cb85c',
          danger: '#f0ad4e',
          error: '#d9534f',
          info: '#5bc0de',
          clean: '#fff'
        },
        {
          primary: '#1f9ed8',
          secondary: '#424242',
          accent: '#75b500',
          danger: '#ff8800',
          error: '#d9534f',
          info: '#9a28cf',
          clean: '#fff'
        }
      ],
      themePresets: [
        { id: 1, name: 'Default' },
        { id: 2, name: 'Theme 1' },
        { id: 3, name: 'Theme 2' },
        { id: 4, name: 'Theme 3' }
      ]
    }
  },
  watch: {
    switch1 (val) {
      if (val) {
        this.$emit('darkTheme', false)
      } else {
        this.$emit('darkTheme', true)        
      }
    },
    userTheme (val) {
      this.$vuetify.theme = this.color[val]
    }
  }
}
</script>
<style scoped>
</style>
