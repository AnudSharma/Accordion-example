<template>
  <div class="accord-wrapper">
    <div v-for="(accordItem,i) in accordata" :key="i">
      <accord-panel>
        <span slot="header">{{accordItem.header}}</span>
        <div>{{accordItem.item}}</div>
      </accord-panel>
    </div>
  </div>
</template>

<script>
import AccordPanel from "../Accordion/AccordPanel";
export default {
  components: {
    AccordPanel
  },
  data() {
    return {
      panels: [],
      open: null,
      accordata: [
        { header: "Head1", item: "We have several panels with the title and a hidden body. When the panel title is clicked, the body's visibility is toggled" },
        { header: "Head2", item: "When one panel opens, any open panel closes. If the open panel is clicked, that panel is closed and no new panels are opened. Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum." },
        { header: "Head3", item: "The panels should open with a nice transition. Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum." }
      ]
    };
  },
  provide() {
    //provide and inject we use to pass the info in grandchild level components-from parent to grandchild
  },
  methods: {
    //to register the panel into the wrapper
    register(panel) {
      this.panels.push(panel);

      //incase we want the first panel to be opened by default-set it to open

    //   if (this.open === null) {
    //     panel.toggle(true);
    //   }
    },

    //unregister the panel if its destroyed

    unregister(panel) {
      if (this.open === panel) {
        this.open = null;
      }
      

      const index = this.panels.findIndex();
      this.panels.splice(index, 1); //remove that panel from the panels array
      
    },
    findIndex(i) {
      return i._uid === this.panel._uid;
    },

    //two use cases:one panel is already opened and need to be closed
    // the already opened panel is to be closed before any other panel is opened
    setOpen(panel, isOpen) {
      for (let i = 0; i < this.panels.length; i++) {
        const item = this.panels[i];

        if (isOpen && item._uid !== panel._uid) {
          item.toggle(false);
        }
      }
      if (isOpen === false) {
        this.open = null;
      } else {
        this.open = panel;
      }
    }
  }
};
</script>