<template>
  <div class="editor-container">
    <div class="editor-header">
      <div class="editor-brand">
        <div class="brand-icon">🐱</div>
        <h1 class="editor-title">CatDown</h1>
      </div>
      <div class="editor-actions">
        <button class="action-btn" @click="handleExport">
          <span class="btn-icon">📥</span>
          <span>导出</span>
        </button>
        <button class="action-btn" @click="handleClear">
          <span class="btn-icon">🗑️</span>
          <span>清空</span>
        </button>
        <button class="action-btn primary" @click="handleSave">
          <span class="btn-icon">💾</span>
          <span>保存</span>
        </button>
      </div>
    </div>
    <div class="editor-body">
      <MdEditor
        v-model="content"
        :theme="theme"
        :preview="preview"
        :toolbars="toolbars"
        :placeholder="'来写下你的Markdown吧😽...'"
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
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  overflow: hidden;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
}

.editor-header {
  height: 70px;
  min-height: 70px;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 32px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.15);
  flex-shrink: 0;
  z-index: 10;
  backdrop-filter: blur(10px);
}

.editor-brand {
  display: flex;
  align-items: center;
  gap: 12px;
  flex-shrink: 0;
}

.brand-icon {
  font-size: 32px;
  filter: drop-shadow(0 2px 4px rgba(0, 0, 0, 0.2));
  animation: bounce 2s ease-in-out infinite;
}

@keyframes bounce {
  0%, 100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-3px);
  }
}

.editor-title {
  font-size: 24px;
  font-weight: 700;
  margin: 0;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  letter-spacing: 0.5px;
  text-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
}

.editor-actions {
  display: flex;
  gap: 16px;
  align-items: center;
  flex-shrink: 0;
}

.action-btn {
  padding: 10px 24px;
  background: rgba(255, 255, 255, 0.95);
  color: #667eea;
  border: none;
  border-radius: 12px;
  cursor: pointer;
  font-size: 14px;
  font-weight: 600;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  white-space: nowrap;
  min-width: 90px;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.action-btn:hover {
  background: white;
  transform: translateY(-2px) scale(1.02);
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.2);
}

.action-btn:active {
  transform: translateY(0) scale(0.98);
}

.action-btn.primary {
  background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
  color: white;
  box-shadow: 0 4px 15px rgba(240, 147, 251, 0.4);
}

.action-btn.primary:hover {
  background: linear-gradient(135deg, #f5576c 0%, #f093fb 100%);
  box-shadow: 0 6px 25px rgba(245, 87, 108, 0.5);
}

.btn-icon {
  font-size: 16px;
  filter: drop-shadow(0 1px 2px rgba(0, 0, 0, 0.1));
}

.editor-body {
  flex: 1;
  overflow: hidden;
  padding: 20px;
  min-height: 0;
  display: flex;
  flex-direction: column;
}

.markdown-editor {
  height: 100%;
  width: 100%;
  border-radius: 16px;
  overflow: hidden;
  flex: 1;
  min-height: 0;
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.2);
  background: white;
}

.markdown-editor :deep(.md-editor) {
  border: none;
  box-shadow: none;
  height: 100%;
  display: flex;
  flex-direction: column;
  border-radius: 16px;
}

.markdown-editor :deep(.md-editor-toolbar-wrapper) {
  border-bottom: 2px solid #f0f0f0;
  background: linear-gradient(180deg, #fafafa 0%, #f5f5f5 100%);
  padding: 12px 16px;
}

.markdown-editor :deep(.md-editor-toolbar) {
  border: none;
  background: transparent;
}

.markdown-editor :deep(.md-editor-toolbar-item) {
  color: #667eea;
  transition: all 0.2s;
}

.markdown-editor :deep(.md-editor-toolbar-item:hover) {
  color: #764ba2;
  background: rgba(102, 126, 234, 0.1);
  border-radius: 6px;
}

.markdown-editor :deep(.md-editor-content-wrapper) {
  flex: 1;
  overflow: auto;
  min-height: 0;
  background: #fafafa;
}

.markdown-editor :deep(.md-editor-content) {
  padding: 32px;
  max-width: 100%;
  overflow-x: hidden;
  background: white;
  border-right: 2px solid #f0f0f0;
}

.markdown-editor :deep(.md-editor-preview) {
  padding: 32px;
  overflow-y: auto;
  overflow-x: hidden;
  background: white;
}

.markdown-editor :deep(.md-editor-preview) h1,
.markdown-editor :deep(.md-editor-preview) h2,
.markdown-editor :deep(.md-editor-preview) h3,
.markdown-editor :deep(.md-editor-preview) h4,
.markdown-editor :deep(.md-editor-preview) h5,
.markdown-editor :deep(.md-editor-preview) h6 {
  color: #667eea;
  margin-top: 24px;
  margin-bottom: 16px;
}

.markdown-editor :deep(.md-editor-preview) h1 {
  font-size: 32px;
  font-weight: 700;
  padding-bottom: 12px;
  border-bottom: 3px solid #667eea;
}

.markdown-editor :deep(.md-editor-preview) h2 {
  font-size: 28px;
  font-weight: 600;
  padding-bottom: 8px;
  border-bottom: 2px solid #e0e0e0;
}

.markdown-editor :deep(.md-editor-preview) h3 {
  font-size: 24px;
  font-weight: 600;
}

.markdown-editor :deep(.md-editor-preview) h4 {
  font-size: 20px;
  font-weight: 600;
}

.markdown-editor :deep(.md-editor-preview) h5 {
  font-size: 18px;
  font-weight: 600;
}

.markdown-editor :deep(.md-editor-preview) h6 {
  font-size: 16px;
  font-weight: 600;
}

.markdown-editor :deep(.md-editor-preview) p {
  margin: 16px 0;
  line-height: 1.8;
  color: #333;
}

.markdown-editor :deep(.md-editor-preview) a {
  color: #667eea;
  text-decoration: none;
  transition: color 0.2s;
}

.markdown-editor :deep(.md-editor-preview) a:hover {
  color: #764ba2;
  text-decoration: underline;
}

.markdown-editor :deep(.md-editor-preview) code {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  padding: 2px 8px;
  border-radius: 4px;
  font-size: 14px;
}

.markdown-editor :deep(.md-editor-preview) pre {
  background: #f5f5f5;
  border-radius: 8px;
  padding: 20px;
  overflow-x: auto;
  border: 2px solid #e0e0e0;
}

.markdown-editor :deep(.md-editor-preview) pre code {
  background: transparent;
  padding: 0;
  color: #333;
}

.markdown-editor :deep(.md-editor-preview) blockquote {
  border-left: 4px solid #667eea;
  padding-left: 20px;
  margin: 20px 0;
  color: #666;
  background: rgba(102, 126, 234, 0.05);
  padding: 16px 20px;
  border-radius: 0 8px 8px 0;
}

.markdown-editor :deep(.md-editor-preview) ul,
.markdown-editor :deep(.md-editor-preview) ol {
  padding-left: 30px;
  margin: 16px 0;
}

.markdown-editor :deep(.md-editor-preview) li {
  margin: 8px 0;
  line-height: 1.6;
}

.markdown-editor :deep(.md-editor-preview) table {
  width: 100%;
  border-collapse: collapse;
  margin: 20px 0;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.markdown-editor :deep(.md-editor-preview) th {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  padding: 12px;
  text-align: left;
  font-weight: 600;
}

.markdown-editor :deep(.md-editor-preview) td {
  padding: 12px;
  border: 1px solid #e0e0e0;
}

.markdown-editor :deep(.md-editor-preview) tr:nth-child(even) {
  background: #f9f9f9;
}

.markdown-editor :deep(.md-editor-preview) tr:hover {
  background: rgba(102, 126, 234, 0.05);
}

.markdown-editor :deep(.md-editor-preview) img {
  max-width: 100%;
  height: auto;
  border-radius: 8px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
  margin: 16px 0;
}

.markdown-editor :deep(.md-editor-preview) hr {
  border: none;
  height: 2px;
  background: linear-gradient(90deg, transparent, #667eea, transparent);
  margin: 32px 0;
}

.markdown-editor :deep(.md-editor-content) {
  font-family: 'Consolas', 'Monaco', 'Courier New', monospace;
  font-size: 15px;
  line-height: 1.8;
  color: #333;
  padding: 32px;
}

.markdown-editor :deep(.md-editor-content-wrapper) {
  position: relative;
}

@media (max-width: 768px) {
  .editor-header {
    height: 60px;
    min-height: 60px;
    padding: 0 16px;
  }

  .brand-icon {
    font-size: 24px;
  }

  .editor-title {
    font-size: 18px;
  }

  .editor-actions {
    gap: 8px;
  }

  .action-btn {
    padding: 8px 12px;
    font-size: 12px;
    min-width: 60px;
  }

  .btn-icon {
    font-size: 14px;
  }

  .editor-body {
    padding: 12px;
  }

  .markdown-editor :deep(.md-editor-content) {
    padding: 20px;
  }

  .markdown-editor :deep(.md-editor-preview) {
    padding: 20px;
  }

  .markdown-editor :deep(.md-editor-preview) h1 {
    font-size: 24px;
  }

  .markdown-editor :deep(.md-editor-preview) h2 {
    font-size: 22px;
  }

  .markdown-editor :deep(.md-editor-preview) h3 {
    font-size: 20px;
  }
}
</style>