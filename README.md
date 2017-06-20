# TagsBox

Tags Box component for Vue with Bulma. Each comma separated value in a textarea input turns into a tag.

![alt text](https://github.com/aislasq/vue-bulma-tagsbox/blob/master/images/image.png "Logo Title Text 1")


## Installation
```
$ npm install https://github.com/aislasq/vue-bulma-tagsbox.git
```

## Usage

#### Props:

* **tags:** The array holding your tags, it is required to correctly show your current tags.
* **tagClass:** The string holding the class of the tag, it is not required, defaults to 'is-primary'.
* **withDeleteButton:** This boolean restricts the delete button inside the tag, defaults to true.

#### Methods: 

* **add-tag:** Called after a tag is validated by the separators, it includes the tag name (input string).
* **remove-tag:** Call after a request to remove a tag with the index.
* **duplicate-tag:** Called when a tag failed the duplicate validation with the name of the tag.

```vue
<template>
  <div>
    <tags-box :tags="tags" 
              tagColor="is-info" 
              @add-tag="val => addTag(val)"
              @remove-tag="val => removeTag(val)"
              @duplicate-tag="val => duplicateTag(val)">
    </tags-box>
  </div>
</template>

<script>
import TagsBox from 'vue-bulma-tagsbox';

export default {
  components: {
    'tags-box': TagsBox
  }
  data: function(){
    return { tags: [] }
  },
  methods: {
    addTag: function(value){
      this.tags.push(tag);
      console.log('Added new Tag: ' + value);
    },
    removeTag: function(value){
      this.tags.splice(index, 1);
      console.log('Removed Tag: ' + value);
    },
    duplicateTag: function(value){
      console.log('Tag already exists: ' + value);
    }
  }
}
</script>
```

## TODO

* Add props for lowercase and case insensitive tags.
* Add props for separators. (Currently only `,` (comma) and `;` (semicolon) work.)

## Badges

![](https://img.shields.io/badge/license-MIT-blue.svg)
![](https://img.shields.io/badge/status-stable-green.svg)
