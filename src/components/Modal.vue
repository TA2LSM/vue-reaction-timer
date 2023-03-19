<!-- Do not give standard HTML keyword names to your components
when you use lowercase letters as a compoennet name or start
naming them with capital letters !!! -->

<template>
  <!-- click.self provides closeModal only works when clicking backdrop
       itself NOT any child components -->
  <div class="backdrop" @click.self="closeModal" >
    <!-- adding another dynamic class according data binding value theme -->
    <!-- <div class="modal" :class="checkTheme(this.theme)">
      <h1>{{ this.header }}</h1>
      <p style="font-weight: bold;">{{ this.text }}</p>
    </div> -->

    <div class="modal" :class="checkTheme(this.theme)">
      <!-- default slot. No Information will be showed when there is no data passed here -->
      <slot>No Information!</slot>

      <div class="actions">
        <!-- named slot -->
        <slot name="modalLinks">
          - No links -
        </slot>
      </div>
    </div>
  </div>
</template>

<script>
  // props object MUST be registered here!
  export default {
    name: 'Modal',

    // props: ['header', 'text', 'theme']
    props: {
      // header: String,
      // text: String,
      theme: String
    },
    
    methods: {
      checkTheme(theme) {
        //                            key: value
        if(theme === "sale") return {sale: theme === 'sale'}
        if(theme === "dark") return {dark: theme === 'dark'}
      },

      // creating custom event named "closeModal". This event will be listened by parent component.
      closeModal() {
        this.$emit('closeModal');
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<!-- <style scoped> -->
<style>
  .modal {
    background: white;
    border-radius: 10px;
    width: 400px;
    padding: 20px;
    margin: 0;
    position: absolute;
    top: 50%;
    left: 50%;
    -ms-transform: translate(-50%, -50%);
    transform: translate(-50%, -50%);
  }

  .backdrop {
    top: 0;
    left: 0;
    position: fixed;
    background: rgba(0,0,0,0.5);
    width: 100%;
    height: 100%;
  }

  /* h1 style owerwrite but all h1 tags will be applied unless you use "<style scoped>" above
    In that case styles in this file will be renamed like this: <h1 data-v-xxxxxxxx> ... 
    But this approach should be used in some specific situations not commonly */
  /* h1 {
    color: #3603cf;
    border: none;
    padding: 0;
  } */

  .modal h1 {
    color: #3603cf;
    border: none;
    padding: 0;
  }

  .modal p {
    font-style: normal;
  }

  .modal.sale {
    background: crimson;
    color: white;
  }
  .modal.sale h1 {
    color: white;
  }
  .modal.dark {
    background: black;
    color: white;
  }
  .modal.dark h1 {
    color: white;
  }

  .modal .actions {
    text-align: center;
    margin: 30px 0 10px 0;
  }
  .modal .actions a {
     padding: 8px;
    border: 2px solid #eee;
    border-radius: 4px;
    text-decoration: none;
    margin: 10px;
  }

  .modal.sale .actions {
    color: white;
  }
  .modal.sale .actions a{
    color: white;
  }
  .modal.dark .actions {
    color: white;
  }
  .modal.dark .actions a{
    color: white;
  }

</style>
