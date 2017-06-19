<template>
    <div class="textarea">
        <span v-for="(tag, index) in tags" class="tag" :class="tagClass">
            <span>{{tag}}</span>
            <button @click="removeTag(index)" title="Removing tag" class="delete is-small"></button>
        </span>
        <input  v-model="input" class="tagsinput"
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
            required: false,
            default: []
        },
        tagClass: {
            type: String,
            required: false,
            default: 'is-primary'
        }
    },
    data: function(params) {
        return {
            input: ''
        }
    },
    methods: {
        addTag: function(value) {
            if (value === null) return;
            if(this.tags.indexOf(value.toUpperCase()) <= -1  ){
                this.$emit('add-tag-failed', value.toUpperCase() );
            }
            if (value !== '') {
                this.tags.push(value.toUpperCase());
                this.$emit('added-tag', value.toUpperCase() );
            }
        },
        removeTag: function(index) {
            let val = this.tags[index];
            this.tags.splice(index, 1);
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
