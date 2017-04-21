<template>
  <component class="list">
    <component class="item"
               v-for="(index, topOffset) in metaDataOfVisibleList"
               :render="rowRender(metaDataOfVisibleList[index], metaDataOfVisibleList[topOffset])">
    </component>
  </component>
</template>

<script>

export default {
  name: 'list',
  props: {
    // items in list
    items: {
      type: Array,
      required: true,
    },
    // width of container
    width: {
      type: Number,
      required: true,
    },
    // height of container
    height: {
      type: Number,
      required: true,
    },
    rowHeight: {
      type: Number, // should recieve function if want dynamic width
      required: true,
    },
    rowRender: { // recieves a style with position absolute (top offset), the index of the list to be rendered
      type: Function,
      required: true,
    },
  },
  data() {
    return {
      scrollTop: 0,
      metaDataOfVisibleList: [],
    };
  },
  methods: {
    // checks height of each array item
    // assuming equal item heights so only checking first
    visibleItems: function (scrollTop, visibleHeight, items, rowHeight) {
      let currTop = scrollTop;
      let addTillReachCurrTop = 0;
      let index = 0;

      // while we havent reached the bottom of the container
      while (addTillReachCurrTop <= currTop + visibleHeight) {
        addTillReachCurrTop += rowHeight;
        index += 1;

        // only push the visible array elements into the metaData
        if (addTillReachCurrTop >= currTop - rowHeight) {
          // metaData returns the indexes and their scrollHeight
          this.metaDataOfVisibleList.push({
            index: index,
            topOffset: addTillReachCurrTop
          })
        }
      }
    }
  }
}
</script>

<style>

</style>
