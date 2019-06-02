<template>
  <div>
    <div :key="item.comment_id" v-for="item in comments">
      <CommentListItem :commentObj="item"/>
    </div>
    <CommentCreate :contentId="contentId" :reloadComments="reloadComments"/>
  </div>
</template>
<script>
import data from "@/data";
import CommentListItem from './CommentListItem';
import CommentCreate from './CommentCreate';
import {findComment} from '../service'

export default {
  name: "CommentList",
  props: {
    contentId: Number
  },
  components: {
    CommentListItem,
    CommentCreate,
  },
  async created() {
    const ret = await findComment({content_id: this.contentId})
    this.comments = ret.data
  },
  data() {
    return {
      comments: [],
    }
  },
  methods: {
    async reloadComments() {
      const ret = await findComment({content_id: this.contentId})
      this.comments = ret.data
    }
  }
};
</script>
