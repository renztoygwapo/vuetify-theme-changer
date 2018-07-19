<template>
  <div class="text-xs-center">
    <v-dialog
      persistent
      v-model="dialog"
      width="500"
    >
      <v-card>
        <v-card-title
          class="headline"
          primary-title
        >
          Report
        </v-card-title>
        <v-card-text>
          {{ report }}
        </v-card-text>

        <v-divider></v-divider>

        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn
            flat
            @click="$emit('closeReportDialog')"
          >
            Cancel
          </v-btn>
          <v-btn
            color="primary"
            flat
            @click="$emit('closeReportDialog')"
          >
            Save
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>

<script>
  module.exports = {
    props: {
      dialog: {
        type: Boolean,
        default: false
      },
      report: {
        type: Object
      }
    }
  }
</script>
