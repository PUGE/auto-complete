<template>
  <div class="autocomplete-puge" contenteditable="true" @blur="blur"></div>
</template>

<script>

export default {
  props: {
    value: Array
  },
  methods: {
    blur (e) {
      let newDomList = []
      const child = e.target.childNodes
      // console.log(child)
      for (let ind = 0; ind < child.length; ind++) {
        // console.log(child[ind])
        if (child[ind].nodeName === 'SPAN') {
          if (child[ind].innerText === ' ') continue
          // 去除首尾空格
          const clear = child[ind].innerText.replace(/(^\s*)|(\s*$)/g, "")
          newDomList.push(clear)
        } else if (child[ind].nodeName === '#text') {
          newDomList.push(child[ind].textContent)
        }
      }
      this.$emit('input', newDomList)
    }
  },
  mounted () {
    if (!this.value) return
    let newHtml = ''
    for (let ind = 0; ind < this.value.length; ind++) {
      newHtml += `<span>&nbsp;</span><span class="content">${this.value[ind]}</span><span>&nbsp;</span>`
    }
    this.$el.innerHTML = newHtml
  },
  watch: {
    'value' (value) {
      if (typeof value !== 'object') return
      let newHtml = ''
      for (let ind = 0; ind < value.length; ind++) {
        newHtml += `<span>&nbsp;</span><span class="content">${value[ind]}</span><span>&nbsp;</span>`
      }
      this.$el.innerHTML = newHtml
    }
  }
}
</script>

<style>
  .autocomplete-puge {
    height: 40px;
    line-height: 40px;
    width: 100%;
    padding: 0 10px;
    overflow: hidden;
    background-color: white;
    border: 1px solid #ccc;
  }
  .autocomplete-puge .content {
    background-color: skyblue;
    margin-right: 5px;
    padding: 2px 5px;
    color: white;
    height: 20px;
    border-radius: 2px;
    line-height: 20px;
  }
</style>
