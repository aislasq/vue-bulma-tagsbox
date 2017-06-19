# TagsBox

Tags Box component for Vue with Bulma. Each comma separated value in a textarea input turns into a tag.

![alt text](https://github.com/aislasq/vue-bulma-tagsbox/images/image.png "Logo Title Text 1")


## Installation
```
$ npm install https://github.com/aislasq/vue-bulma-tagsbox.git
```

## Usage

#### Props:

* **tags:** The array holding your tags, it is not required.
* **tagClass:** The string holding the class of the tag, it is not required, defaults to 'is-primary'.
* **withDeleteButton:** This boolean restricts the delete button inside the tag, defaults to true.

#### Methods: 

* **added-tag:** Called after a tag is added to the array with the tag name.
* **removed-tag:** Called after a tag is removed from the array with the tag name.
* **add-tag-duplicate:** Called after a tag failed to be added to the array because it is duplicated.

```vue
<template>
  <div>
    <tags-box :tags="tags" 
              tagColor="is-info" 
              @added-tag="val => addedNewTag(val)"
              @removed-tag="val => removedTag(val)"
              @add-tag-duplicate="val => duplicateTag(val)">
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
    addedNewTag: function(value){
      console.log('Added new Tag: ' + value);
    },
    removedTag: function(value){
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
