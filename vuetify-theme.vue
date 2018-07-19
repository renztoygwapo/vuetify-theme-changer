<template>
  <v-layout>
    <v-flex xs12 sm12 md12 lg12 class="ml-3 mr-3 mb-3">
      <v-card :flat="isFlat">
        <v-toolbar color="primary" :flat="isFlat">
          <v-toolbar-title class="white-text">
            {{ componentTitle }}
          </v-toolbar-title>
          <v-spacer></v-spacer>
        </v-toolbar>
        <v-card-text>
          <v-layout row wrap>
            <v-flex xs12 md3>
              <v-subheader>
                Theme
              </v-subheader>
              <v-switch
                :label="isDark ? 'Light' : 'Dark'" v-model="isDark">
              </v-switch>
              <v-subheader>
                Flat
              </v-subheader>
               <v-switch
                :label="isFlat ? 'Flat' : 'Not Flat'" v-model="isFlat">
              </v-switch>
            </v-flex>
            <v-flex xs12 md3>
              <v-subheader>
                Colors
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
            <v-flex xs12 md3>
            </v-flex>
          </v-layout>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn
            :dark="!isDark"
            :flat="isFlat"
            color="primary"
            :loading="loading"
            :disabled="loading"
            @click="saveChanges"
          >Save Changes</v-btn>
        </v-card-actions>
      </v-card>
    </v-flex>
  </v-layout>
</template>
<script>

module.exports = {
  props: {
    componentTitle: {
      type: String,
      default: 'Change Theme'
    },
    theme: {
      type: Object
    }
  },
  computed: {
    loading () {
      return this.$store.state.appUI.loading
    }
  },
  created () {
    this.isDark = !this.theme.isDark
    this.isFlat = this.theme.isFlat
    this.$vuetify.theme = this.theme.color
    this.userTheme = this.theme.userTheme
  },
  methods: {
    saveChanges () {
      const color = this.color[this.userTheme]
      this.themeObj = {
        isDark: !this.isDark,
        isFlat: this.isFlat,
        color: color,
        userTheme: this.userTheme
      }
      this.$emit('save', this.themeObj)
    }
  },
  data: function () {
    return {
      isFlat: false,
      themeObj: {},
      isDark: true,
      userTheme: 0,
      color: [
        {
          primary: '#f44336',
          secondary: '#F50057',
          success: '#5cb85c',
          accent: '#008080',
          danger: '#d53182',
          error: '#b71c1c',
          info: '#1c89d5',
          clean: '#fff'
        },
        {
          primary: '#1c095E',
          secondary: '#914679',
          success: '#5cb85c',
          accent: '#e23d80',
          danger: '#d53182',
          error: '#EF5B8C',
          info: '#1c89d5',
          clean: '#fff'
        },
        {
          primary: '#df691a',
          secondary: '#4e5d6c',
          success: '#5cb85c',
          accent: '#5cb85c',
          danger: '#f0ad4e',
          error: '#d9534f',
          info: '#5bc0de',
          clean: '#fff'
        },
        {
          primary: '#1f9ed8',
          secondary: '#424242',
          success: '#5cb85c',
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
    isFlat (val) {
      if (val) {
        this.$emit('toFlat', true)
      } else {
        this.$emit('toFlat', false)
      }
    },
    isDark (val) {
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
