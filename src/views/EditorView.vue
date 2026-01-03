<template>
  <div class="editor-container">
    <div class="editor-header">
      <h1 class="editor-title">CatDown</h1>
      <div class="editor-actions">
        <button class="action-btn" @click="handleExport">导出</button>
        <button class="action-btn" @click="handleClear">清空</button>
        <button class="action-btn primary" @click="handleSave">保存</button>
      </div>
    </div>
    <div class="editor-body">
      <MdEditor
        v-model="content"
        :theme="theme"
        :preview="preview"
        :toolbars="toolbars"
        :placeholder="'开始编写你的Markdown文档...'"
        @save="handleSave"
        class="markdown-editor"
      />
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { MdEditor } from 'md-editor-v3'
import 'md-editor-v3/lib/style.css'

const content = ref('')
const theme = ref('light')
const preview = ref(true)
const toolbars = [
  'bold',
  'underline',
  'italic',
  'strikeThrough',
  '-',
  'title',
  'sub',
  'sup',
  'quote',
  'unorderedList',
  'orderedList',
  'task',
  '-',
  'codeRow',
  'code',
  'link',
  'image',
  'table',
  '-',
  'revoke',
  'next',
  'save',
  '=',
  'pageFullscreen',
  'fullscreen',
  'preview',
  'htmlPreview',
  'catalog'
]

const handleSave = () => {
  console.log('保存内容:', content.value)
  alert('保存成功！')
}

const handleExport = () => {
  const blob = new Blob([content.value], { type: 'text/markdown' })
  const url = URL.createObjectURL(blob)
  const a = document.createElement('a')
  a.href = url
  a.download = 'document.md'
  a.click()
  URL.revokeObjectURL(url)
}

const handleClear = () => {
  if (confirm('确定要清空内容吗？')) {
    content.value = ''
  }
}
</script>

<style scoped>
.editor-container {
  display: flex;
  flex-direction: column;
  height: 100vh;
  width: 100%;
  background-color: #ffffff;
  overflow: hidden;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
}

.editor-header {
  height: 60px;
  min-height: 60px;
  background-color: #409eff;
  color: white;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 24px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  flex-shrink: 0;
  z-index: 10;
}

.editor-title {
  font-size: 20px;
  font-weight: 600;
  margin: 0;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.editor-actions {
  display: flex;
  gap: 12px;
  align-items: center;
  flex-shrink: 0;
}

.action-btn {
  padding: 8px 20px;
  background-color: rgba(255, 255, 255, 0.9);
  color: #409eff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 14px;
  font-weight: 500;
  transition: all 0.2s;
  white-space: nowrap;
  min-width: 80px;
}

.action-btn:hover {
  background-color: white;
  transform: translateY(-1px);
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.15);
}

.action-btn.primary {
  background-color: #67c23a;
  color: white;
}

.action-btn.primary:hover {
  background-color: #85ce61;
}

.editor-body {
  flex: 1;
  overflow: hidden;
  padding: 0;
  min-height: 0;
  display: flex;
  flex-direction: column;
}

.markdown-editor {
  height: 100%;
  width: 100%;
  border: none;
  flex: 1;
  min-height: 0;
}

.markdown-editor :deep(.md-editor) {
  border: none;
  box-shadow: none;
  height: 100%;
  display: flex;
  flex-direction: column;
}

.markdown-editor :deep(.md-editor-content-wrapper) {
  flex: 1;
  overflow: auto;
  min-height: 0;
}

.markdown-editor :deep(.md-editor-content) {
  padding: 24px;
  max-width: 100%;
  overflow-x: hidden;
}

.markdown-editor :deep(.md-editor-preview) {
  padding: 24px;
  overflow-y: auto;
  overflow-x: hidden;
}

@media (max-width: 768px) {
  .editor-header {
    padding: 0 16px;
  }

  .editor-title {
    font-size: 16px;
  }

  .editor-actions {
    gap: 8px;
  }

  .action-btn {
    padding: 6px 12px;
    font-size: 12px;
    min-width: 60px;
  }

  .markdown-editor :deep(.md-editor-content) {
    padding: 16px;
  }

  .markdown-editor :deep(.md-editor-preview) {
    padding: 16px;
  }
}
</style>