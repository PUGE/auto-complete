<template>
  <div class="autocomplete-puge" contenteditable="true" @blur="blur"></div>
</template>

<script>

export default {
  methods: {
    blur (e) {
      let newDomList = []
      let newHtml = ''
      const child = e.target.childNodes
      // console.log(child)
      for (let ind = 0; ind < child.length; ind++) {
        // console.log(child[ind])
        if (child[ind].nodeName === 'SPAN') {
          if (child[ind].innerText === ' ') continue
          newDomList.push(child[ind].innerText)
          // 去除首尾空格
          const clear = child[ind].innerText.replace(/(^\s*)|(\s*$)/g, "")
          newHtml += `<span>&nbsp;</span><span class="content">${child[ind].innerText}</span><span>&nbsp;</span>`
        } else if (child[ind].nodeName === '#text') {
          newDomList.push(child[ind].textContent)
          newHtml += `<span>&nbsp;</span><span class="content">${child[ind].textContent}</span><span>&nbsp;</span>`
        }
      }
      e.target.innerHTML = newHtml
      this.$emit('change', newDomList)
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
