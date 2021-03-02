<template>
  <div class="autocomplete">
    <label class="label" for="input">Choose your favourite month</label>
    <input
      type="text"
      id="input"
      class="input"
      @input="onChange"
      v-model="search"
    />
    <ul
      v-show="isOpen"
      class="autocomplete-results"
    >
      <li
        v-for="(result, i) in results"
        :key="i"
        @click="setChoice(result)"
        class="autocomplete-result"
      >
        {{ result }}
      </li>
    </ul>
  </div>
</template>

<script>
  export default {
    name: 'autocomplete',

    props: {
      items: {
        type: Array,
        required: false,
      },
    },

    data() {
      return {
        results: [],
        search: '',
        isOpen: false,
      };
    },

    methods: {
      onChange() {
        this.$emit('input', this.search);
        this.getItems();
        this.isOpen = true;
    
      },

      getItems() {
        this.results = this.items.filter((item) => {
          return item.toLowerCase().indexOf(this.search.toLowerCase()) > -1;
        });
      },

      setChoice(result) {
        this.search = result;
        this.isOpen = false;
      },
      
      handleClickOutside(e) {
        if (!this.$el.contains(e.target)) {
          this.isOpen = false;
          this.search = '';
        }
      }
    },
    mounted() {
      document.addEventListener('click', this.handleClickOutside)
    },
    destroyed() {
      document.removeEventListener('click', this.handleClickOutside)
    }
  };
</script>

<style lang="scss">
  .autocomplete {
    display: flex;
    flex-direction: column;
    padding: 60px;
    
  }
  .label {
    margin-bottom: 10px;
    font-size: 14px;
  }
  .input {
    width: 300px;
    border: 1px solid gray;
    border-radius: 3px;
  }
  .autocomplete-results {
    padding: 0;
    margin: 0;
    border: 1px solid #eeeeee;
    height: auto;
    overflow: auto;
    width: 306px;
  }

  .autocomplete-result {
    list-style: none;
    text-align: left;
    padding: 4px 2px;
    cursor: pointer;
    
    &:hover {
    background-color: #c2bdbd;
    color: white;
  }
  }
</style>