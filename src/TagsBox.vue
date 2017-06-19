<template>
    <div class="textarea">
        <span v-for="(tag, index) in tags" class="tag is-primary">
            <span>{{tag}}</span>
            <button @click="removeTag(index)" title="Removing tag" class="delete is-small"></button>
        </span>
        <input  v-model="input" class="tagsinput"
                @keyup.comma="splitTagComma" 
                @keyup.semicolon="splitTagSemiColon"
                @keydown.delete="backspace" >
    </div>
</template>

<script>
Vue.config.keyCodes.comma = 188
Vue.config.keyCodes.semicolon = 186
Vue.config.keyCodes.backspace = 8

export default {
    props: ['tags'],
    data: function(params) {
        return {
            input: ''
        }
    },
    methods: {
        addTag: function(value) {
            if (value === null) return;
            if(this.names.indexOf(value.toUpperCase()) <= -1  )){
                this.$emit('add-tag-failed', value.toUpperCase() );
            }
            if (value !== '') {
                this.names.push(value.toUpperCase());
                this.$emit('added-tag', value.toUpperCase() );
            }
        },
        removeTag: function(index) {
            let val = this.names[index];
            this.names.splice(index, 1);
            this.$emit('removed-tag', val);
        },
        backspace: function(value){
    	    if(this.input === ''){
      	        this.removeTag(-1);
            }
        },
        splitTagComma: function(value){
            this.input.split(",").forEach((e) => this.addTag(e))
            this.input = ''
        },
        splitTagSemiColon: function(){
            this.input.split(";").forEach((e) => this.addTag(e))
            this.input = ''
        }
  }
}
</script>
<style>
    div.textarea span.tag {
        float: left;
    }

    input.tagsinput {
        width: auto;
        margin: 0px;
        border: 1px solid transparent;
        padding: 5px;
        background: transparent;
        color: #000;
        outline: 0px;
        margin-right: 5px;
        margin-bottom: 5px;
        display: block;
        float: left;
    }
</style>
