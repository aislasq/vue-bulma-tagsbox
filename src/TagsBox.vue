<template>
    <div class="textarea" @click="focusInput" style="cursor: text;">
        <span v-for="(tag, index) in tags" :class="tagClass" class="tag" style="float: left;">
            <span>{{tag}}</span>
            <button v-if="withDeleteButton" type="button" @click="removeTag(index)" title="Remove tag" class="delete is-small"></button>
        </span>
        <input  class="tagsinput" ref='inputTextBox' v-model="input" 
                @keyup.188="splitTagComma" 
                @keyup.186="splitTagSemiColon"
                @keydown.8="backspace" >
    </div>
</template>

<script>

export default {
    props: {
        tags: {
            type: Array,
            required: true
        },
        tagClass: {
            type: String,
            required: false,
            default: 'is-primary'
        },
        withDeleteButton: {
            type: Boolean,
            required: false,
            default: true
        }
    },
    data: function(params) {
        return {
            input: ''
        }
    },
    methods: {
        focusInput: function(){
            this.$refs.inputTextBox.focus();
        },
        addTag: function(value) {
            if (value === null || value === '') return;

            let toAdd = value.toUpperCase();
            if(this.tags.indexOf(toAdd) == -1 ){
                this.$emit('add-tag', toAdd );
            }
            else{
                this.$emit('duplicate-tag', toAdd );
            }
        },
        removeTag: function(index) {
            this.$emit('remove-tag', index);
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
    input.tagsinput {
        margin: 0px;
        width: 15%;
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
