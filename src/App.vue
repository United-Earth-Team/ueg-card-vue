<template>
  <div class="flex flex-wrap justify-center my-20 mx-5">
    <div class="lg:w-7/12 xl:w-1/3 w-full justify-center lg:mb-0 mb-10 lg:mr-10">
      <div class="w-full rounded-xl bg-zinc-100 bg-clip-border drop-shadow-2lg">
        <div class="mx-auto flex flex-wrap container">
          <div class="lg:px-10 pb-5 px-5 w-full justify-center">
            <h4 :class="$tt('headline4')" id="font-bc">UEG 名牌生成器</h4>
            <ui-form item-margin-bottom="16">
              <ui-form-field>
                <ui-textfield fullwidth outlined required v-model="surname">姓 / Surname</ui-textfield>
              </ui-form-field>
              <ui-form-field>
                <ui-textfield fullwidth outlined required v-model="givenname">名 / Given Name</ui-textfield>
              </ui-form-field>
              <ui-form-field>
                <ui-textfield fullwidth outlined required v-model="position">职位 / Position</ui-textfield>
              </ui-form-field>
            </ui-form>
            <div class="grid grid-flow-col mb-4 whitespace-pre-wrap break-keep">
            <ui-file class="col-span-2" accept="image/*" @change="balmUI.onChange('files', $event)"
              :text="files[0] ? '更换 / Change' :'选择头像 / Select Avator'"></ui-file>
            <ui-button class="col-span-1" v-if="files[0]" outlined icon="download" @click="getDownload">保存 / Save</ui-button></div>
            <div class="w-full mt-5">
              <Readme></Readme>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="lg:w-4/12 xl:w-1/4 w-10/12 bg-zinc-100 border-solid border-x-8 border-white rounded-lg drop-shadow-2lg">
      <div class="justify-center mt-2">
        <CardRender :surname="getAttrs['surname']" :givenname="getAttrs['givenname']" :position="getAttrs['position']"
          :avator="getAttrs['avator']" />
      </div>

    </div>
  </div>
</template>


<script>
import CardRender from './components/CardRender.vue';
import Readme from './components/Readme.vue';
import { useEvent } from 'balm-ui';
import cardcss from './card.css?inline'


export default {
  data() {
    return {
      surname: "ZHOU",
      givenname: "ZHEZHI",
      position: "PERMANENT REPRESENTATIVE",
      balmUI: useEvent(),
      files: [],
      download: {
        filename: null,
        url: null
      },
    }
  },
  components: {
    CardRender,
    Readme
  },
  computed: {
    getAttrs() {
      return {
        surname: this.surname.toUpperCase(),
        givenname: this.givenname.toUpperCase(),
        position: this.position.toUpperCase(),
        avator: this.files[0] ? this.files[0].sourceFile : null
      }
    },
  },
  methods: {
    async getDownload() {
      let timenow = new Date().valueOf()
      let filename = `${this.getAttrs['surname']}-${this.getAttrs['givenname']}-${timenow}.png`
      const output = { "name": filename, "width": 2800, "height": 4000 }
      let uegcard = document.querySelector('#ueg-card')
      if (uegcard) {
        uegcard = uegcard.cloneNode(true)
        let cssNode = document.createElement('style')
        cssNode.innerHTML = cardcss
        uegcard.appendChild(cssNode)
        const uriData = `data:image/svg+xml;base64,${btoa(new XMLSerializer().serializeToString(uegcard))}`

        const img = new Image()
        img.src = uriData
        img.onload = () => {
          const canvas = document.createElement("canvas");
          [canvas.width, canvas.height] = [output.width, output.height]
          const ctx = canvas.getContext("2d")
          ctx.drawImage(img, 0, 0, output.width, output.height)

          // 👇 download
          const a = document.createElement("a")
          const quality = 1.0 // https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/imageSmoothingQuality
          a.href = canvas.toDataURL("image/png", quality)
          a.download = filename
          a.append(canvas)
          a.click()
          a.remove()
        }
      }
    }
  }
}


</script>


<style scoped>

</style>