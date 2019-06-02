<template>
  <div>
    <b-input v-model="subject" placeholder="제목을 입력해 주세요"></b-input>
    <b-form-textarea v-model="context" placeholder="내용을 입력해 주세요" rows="3" max-rows="6"></b-form-textarea>
    <b-button @click="updateMode ? updateContent() : uploadContent()">저장</b-button>
    <b-button @click="cancle">취소</b-button>
  </div>
</template>
<script>
import data from "@/data";
import { addContent, modifyContent, findContent } from "../service";

export default {
  name: "Create",
  data() {
    return {
      subject: "",
      context: "",
      userId: 1,
      createdAt: "2019-04-17 11:32:42",
      updatedAt: null,
      updateObject: null,
      updateMode: this.$route.params.contentId > 0 ? true : false
    };
  },
  async created() {
    if (this.$route.params.contentId > 0) {
      const ret = await findContent({ content_id: Number(this.$route.params.contentId)})
      const {data} = ret;
      this.subject = data.title;
      this.context = data.context;
    }
  },
  methods: {
    async uploadContent() {
      let items = data.Content.sort((a, b) => {
        return b.content_id - a.content_id;
      });
      const content_id = items[0].content_id + 1;
      await addContent({
        user_id: this.userId,
        title: this.subject,
        context: this.context
      });
      this.$router.push({
        path: "/board/free/"
      });
    },
    async updateContent() {
      await modifyContent({
        context_id: Number(this.$route.params.contentId),
        title: this.subject,
        context: this.context
      });
      this.$router.push({
        path: "/board/free/"
      });
    },
    cancle() {
      this.$router.push({
        path: "/board/free/"
      });
    }
  }
};
</script>