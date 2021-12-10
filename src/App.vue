<template>
  <div id="app">
    <BlocklyComponent id="blockly" :options="options" ref="foo"></BlocklyComponent>
    <p id="code">
      <button v-on:click="showCode()">Show JavaScript</button>
      <pre v-html="code"></pre>
    </p>
  </div>
</template>

<script>
import BlocklyComponent from './components/BlocklyComponent.vue'
import Blockly from 'blockly';
import BlocklyJS from 'blockly/javascript';

Blockly.Blocks['maze_moveForward'] = {
  /**
   * Block for moving forward.
   * @this {Blockly.Block}
   */
  init: function() {
    this.jsonInit({
      "message0": "Move forward",
      "previousStatement": null,
      "nextStatement": null,
      "colour": 230,
      "tooltip": "This moves the character forward in the direction the are currently facing"
    });
  }
};

Blockly.JavaScript['maze_moveForward'] = function(block) {
  return 'moveForward(\'block_id_' + block.id + '\');\n';
};

export default {
  name: 'app',
  components: {
    BlocklyComponent
  },
  data(){
    return {
      code: '',
      options: {
        media: 'media/',
        grid:
          {
            spacing: 25,
            length: 3,
            colour: '#ccc',
            snap: true
          },
        toolbox:
        `<xml>
          <block type="maze_moveForward"></block>
        </xml>`
      }
    }
  },
  methods: {
    showCode() {
      this.code = BlocklyJS.workspaceToCode(this.$refs["foo"].workspace);
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

html, body {
  margin: 0;
}

#code {
  position: absolute;
  right: 0;
  top: 0;
  bottom: 0;
  width: 50%;
  margin: 0;
  background-color: beige;
}

#blockly {
  position: absolute;
  left: 0;
  top: 0;
  bottom: 0;
  width: 50%;
}
</style>
