<template>
  <div class="comment-create">
    <b-input-group :prepend="name" class="mt-3">
      <b-form-textarea
        id="textarea"
        v-model="context"
        :placeholder="isSubComment ? '덧글에 덧글을 달아주세요~!' : '코멘트를 달아주세요~!'"
        rows="3"
        max-rows="6"
      ></b-form-textarea>
      <b-input-group-append>
        <b-button variant="info" @click="isSubComment ? createSubComment() : createComment()">작성하기</b-button>
      </b-input-group-append>
    </b-input-group>
  </div>
</template>
<script>
import data from "@/data";
import { addComment, addSubComment } from "../service";

export default {
  name: "CommentCreate",
  props: {
    contentId: Number,
    reloadComments: Function,
    reloadSubComments: Function,
    subCommentToggle: Function,
    isSubComment: Boolean,
    commentId: Number
  },
  data() {
    return {
      name: "르라나",
      context: ""
    };
  },
  methods: {
    async createComment() {
      await addComment({ user_id: 1, content_id: this.contentId, context:this.context });
      this.reloadComments();
      this.context = "";
    },
    async createSubComment() {
      await addSubComment({ user_id: 1, comment_id: this.commentId, context:this.context });
      this.reloadSubComments();
      this.subCommentToggle();
      this.context = "";
    }
  }
};
</script>
<style scoped>
.comment-create {
  display: flex;
  margin-bottom: 1em;
}
</style>
