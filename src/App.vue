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
            <ui-button class="col-span-1" outlined icon="download" @click="getDownload">保存 / Save</ui-button></div>
            <div class="w-full mt-5">
              <Readme></Readme>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="lg:w-4/12 xl:w-1/4 w-10/12 bg-zinc-100 border-solid border-x-8 border-white rounded-lg drop-shadow-2lg">
      <div class="justify-center mt-2">
        <CardRender ref="uegWorkCardRef" :surname="getAttrs['surname']" :givenname="getAttrs['givenname']" :position="getAttrs['position']"
          :avator="getAttrs['avator']" />
      </div>

    </div>
  </div>
</template>

<script>
import CardRender from './components/CardRender.vue';
import Readme from './components/Readme.vue';
import { useEvent } from 'balm-ui';
import * as htmlToImage from 'html-to-image';

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
      const timeNow = new Date().valueOf()
      const filename = `${this.getAttrs['surname']}-${this.getAttrs['givenname']}-${timeNow}.png`
      const uegWorkCardElement = this.$refs.uegWorkCardRef.$el
      const imageOptions = {width:1984.3, height:2834.6}

      if (uegWorkCardElement) {
        const dataUrl = await htmlToImage.toPng(uegWorkCardElement, imageOptions);
        const a = document.createElement('a');
        a.href = dataUrl;
        a.download = filename;
        a.click();
        a.remove();
      }
    }
  }
}


</script>


<style scoped>

</style>