<template>
  <div>
    <q-card style="width: 100%">
      <div class="bg-red">
        <div class="q-pa-md text-white" style="font-size: 18px;">
          Flag Question
        </div>
      </div>
      <div>
        <div class="q-pa-md text-grey">
          Hi there! Thanks for bringing the issue to us. Appreciate if you can
          provide more information about this error on this question !
        </div>
      </div>
      <q-card-section>
        <div class="column q-gutter-x-sm">
          <div class="row">
            <div class="col-4 text-grey-9" style="font-size: 18px;">
              Issue:
            </div>
            <div class="col-8 bg-grey-3" style="border-radius: 10px;">
              <q-input borderless class="q-px-md" v-model="titleInput">
              </q-input>
            </div>
          </div>
          <div class="q-pt-sm">
            <div class="row">
              <div class="col-4 text-grey-9" style="font-size: 18px;">
                Comments:
              </div>
              <div class="col-8 bg-grey-3" style="border-radius: 10px;">
                <q-input
                  type="textarea"
                  class="q-px-md"
                  borderless
                  v-model="inputDescriptions"
                >
                </q-input>
              </div>
            </div>
          </div>
        </div>
      </q-card-section>
      <q-card-section>
        <div class="row q-gutter-x-sm">
          <div class="col-8">
            <q-btn
              style="height: 50px; border-radius: 10px;"
              class="full-width bg-red"
              v-close-popup
              flat
              color="white"
              label="Cancel"
            />
          </div>
          <div class="col">
            <q-btn
            @click="closeModal"
              style="height: 50px; border-radius: 10px;"
              class="full-width bg-blue"
              v-close-popup
              flat
              color="white"
              label="Submit"
            />
          </div>
        </div>
      </q-card-section>
    </q-card>
  </div>
</template>

<script>
export default {
  data () {
    return {
      titleInput: '',

      inputDescriptions: ''
    }
  },
  methods: {
    closeModal () {
      this.$q.notify({
        color: 'green-4',
        textColor: 'white',
        icon: 'cloud_done',
        message: 'Submitted'
      })
    }
  }
}
</script>

<style></style>
