<script setup lang="ts">
import { onMounted, ref } from 'vue'

const showPopup = ref(true) // 弹窗显示状态

const closePopup = () => {
  showPopup.value = false // 关闭弹窗
  sessionStorage.setItem('popupShown', 'true') // 将弹窗已显示的状态保存到sessionStorage中
}

onMounted(() => {
  const popupShown = sessionStorage.getItem('popupShown')
  if (popupShown && popupShown === 'true')
    showPopup.value = false // 如果弹窗已经显示过了，则将showPopup设置为false，不再弹出弹窗
})
</script>

<template>
  <div>
    <div v-if="showPopup" class="popup">
      <!-- 弹窗内容 -->
      <p class="popup-title">
        欢迎使用Xu-ChatGPT
      </p>
      <h1 class="popup-message">
        &emsp;&emsp;注意：此版本具有聊天记录自动存储功能，为避免信息泄露，请务必在使用结束后点击聊天框左侧的删除按钮将聊天记录删除!
      </h1>
      <button class="popup-close-button" @click="closePopup">
        我已知晓
      </button>
    </div>
    <div v-if="showPopup" class="overlay" />
  </div>
</template>

<style>
.popup {
  position: fixed;
  top: 40%;
  left: 50%;
  transform: translate(-50%, -50%);
  background: #ffffff;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.15);

  /* 设置较高的 z-index 值 */
  z-index: 9999;
}

.popup-title {
  text-align: center;
  font-size: 24px;
  margin-bottom: 10px;
}

.popup-message {
  font-size: 18px;
  margin-bottom: 10px;
}

.popup-close-button {
  background: #ffffff;
  border: 2px solid #cccccc;
  border-radius: 4px;
  padding: 4px 8px 4px 8px;
  font-size: 16px;
  cursor: pointer;
  display: block;
  margin: 10px auto 0px auto;
  transition: background-color 0.3s ease;
}

.popup-close-button:hover {
  background-color: #18a058;
}

.overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.6);
  z-index: 9998;
  pointer-events: auto;
  /* 启用指针事件，阻止用户与下方元素交互 */
}
</style>
