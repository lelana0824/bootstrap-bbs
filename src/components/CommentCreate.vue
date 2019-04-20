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

export default {
  name: "CommentCreate",
  props: {
    contentId: Number,
    reloadComments: Function,
    reloadSubComments: Function,
    subCommentToggle: Function,
    isSubComment: Boolean,
    commentId: Number,
  },
  data() {
    return {
      name: "르라나",
      context: ""
    };
  },
  methods: {
    createComment() {
      const comment_id = data.Comment[data.Comment.length - 1].comment_id + 1;
      data.Comment.push({
        comment_id: comment_id,
        user_id: 1,
        content_id: this.contentId,
        context: this.context,
        created_at: "2019-04-19 14:11:11",
        updated_at: null
      });
      this.reloadComments();
      this.subCommentToggle();
      this.context = "";
    },
    createSubComment() {
      const subcomment_id = data.SubComment[data.SubComment.length - 1].subcomment_id + 1;
      data.SubComment.push({
        subcomment_id: subcomment_id,
        comment_id: this.commentId,
        user_id: 1,
        context: this.context,
        created_at: "2019-04-19 16:22:11",
        updated_at: null
      });
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
