<template>
  <div class="wrapper">
    <div class="wrapper-content">
      <section>
        <div class="container">
          <button class="btn btnPrimary" @click="modalFirst =! modalFirst">Show fitrst modal</button>

          <!-- first modal -->

          <modals title="First Modal" v-show="modalFirst" @close="modalFirst = false">
            <div slot="body">
              <p>Text TextText Text Text Text</p>
              <button class="btn btnPrimary" @click="modalFirst =! modalFirst">Well done!!</button>
            </div>
          </modals>
          <!-- second modal -->
          <button
            class="btn btnPrimary"
            @click="modalSecond.show =! modalSecond.show"
          >Show modal with form</button>
          <modals
            title="Modal with form"
            v-show="modalSecond.show"
            @close="closeSecondModal"
          >
            <div slot="body">
              <!-- <p>Text TextText Text Text Text </p> -->
              <form @submit.prevent="submitSecondForm">
                <label>Name:</label>
                <input type="text" required v-model="modalSecond.name" />
                <label>Email:</label>
                <input type="email" required v-model="modalSecond.email" />
                <button class="btn btnPrimary">Submit</button>
              </form>
            </div>
          </modals>

          <!-- Modal with validate -->
          <button
            class="btn btnPrimary"
            @click="modalValidate =! modalValidate"
          >Show modal with form + validate</button>
          <modalValidate v-show="modalValidate" @close="$refs.ModalValidate.resetModalValidate(), modalValidate = false" ref = "ModalValidate"/>
        </div>
      </section>
    </div>
  </div>
</template>

<script>
import modals from "@/components/UI/Modal.vue";
import modalValidate from "@/components/ModalValidate.vue";

export default {
  components: {
    modals,
    modalValidate
  },

  data() {
    return {
      modalFirst: false,
      modalSecond: {
        show: false,
        name: "",
        email: ""
      },
      modalValidate: false
    };
  },

// methods


  methods: {
    submitSecondForm() {
      console.log({
        name: this.modalSecond.name,
        email: this.modalSecond.email
      });
      (this.modalSecond.name = ""),
        (this.modalSecond.email = ""),
        (this.modalSecond.show = false);
    },

    closeSecondModal(){
          (this.modalSecond.name = ""),
        (this.modalSecond.email = ""),
        (this.modalSecond.show = false);
    },
  }
};
</script>

<style>
</style>
