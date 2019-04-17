<template>
  <div>
    <b-input v-model="subject" placeholder="제목을 입력해 주세요"></b-input>
    <b-form-textarea
      v-model="context"
      placeholder="내용을 입력해 주세요"
      rows="3"
      max-rows="6"
    ></b-form-textarea>
    <b-button @click="updateMode ? updateContent() : uploadContent()">저장</b-button>
    <b-button @click="cancle">취소</b-button>
  </div>
</template>
<script>
import data from '@/data'

export default {
  name: 'Create',
  data() {
    return {
      subject: '',
      context: '',
      userId: 1,
      createdAt: '2019-04-17 11:32:42',
      updatedAt: null,
      updateObject: null,
      updateMode: this.$route.params.contentId > 0 ? true : false
    }
  },
  created() {
    if (this.$route.params.contentId > 0) {
      const contentId = Number(this.$route.params.contentId)
      this.updateObject = data.Content.filter(item => item.content_id === contentId)[0]
      this.subject = this.updateObject.title;
      this.context = this.updateObject.context;
    }
  },
  methods: {
    uploadContent() {
      let items = data.Content.sort((a,b) => {return b.content_id - a.content_id})
      const content_id = items[0].content_id + 1
      data.Content.push({
        content_id: content_id,
        user_id: this.userId,
        title: this.subject,
        context: this.context,
        created_at: this.createdAt,
        updated_at: null
      })
      this.$router.push({
        path: '/board/free/'
      })
    },
    updateContent() {
      this.updateObject.title = this.subject;
      this.updateObject.context = this.context;
      this.$router.push({
        path: '/board/free/'
      })
    },
    cancle() {
      this.$router.push({
        path: '/board/free/'
      })
    }
  }
}
</script>