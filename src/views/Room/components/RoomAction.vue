<!-- note: 
1.async await 
2. defineProps,defineEmits 
3.van-filed,van-uploader -->

<template>
  <div class="room-action">
    <van-field
      type="text"
      class="input"
      v-model="msg"
      @keydown.enter.prevent="sendText"
      placeholder="发送消息"
      :disabled="disabled"
    />
    <van-uploader :after-read="sendImage" :disabled="disabled">
      <cp-icon name="consult-img" />
    </van-uploader>
  </div>
</template>
<script setup lang="ts">
import { uploadImage } from '@/services/consult'
import type { Image } from '@/types/consult'
import { showLoadingToast } from 'vant'
import type { UploaderAfterRead } from 'vant/lib/uploader/types'
import { ref } from 'vue'
defineProps(['disabled'])
let emit = defineEmits(['send-text', 'send-image'])
let msg = ref('')
let sendImage = async (file: any) => {
  console.log(file)
  // let res = await uploadImage(file.file);
  // console.log(res.data);
  const url =
    'http://yjy-teach-oss.oss-cn-beijing.aliyuncs.com/consult/production/20250503/7152684074500096.png'
  emit('send-image', { url: url })
}
let sendText = () => {
  emit('send-text', msg.value)
  msg.value = ''
}
</script>
<style lang="scss" scoped>
.room-action {
  position: fixed;
  left: 0;
  bottom: 0;
  width: 100%;
  height: 60px;
  background-color: #fff;
  display: flex;
  align-items: center;
  padding: 0 16px;
  z-index: 1;
  box-sizing: border-box;
  .input {
    background-color: var(--cp-bg);
    border: none;
    border-radius: 25px;
    margin-right: 10px;
    padding: 8px 15px;
  }
  .cp-icon {
    width: 24px;
    height: 24px;
  }
}
</style>
