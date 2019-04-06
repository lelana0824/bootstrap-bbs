<template>
  <div>
    <b-table striped hover :items="items" :fields="fields"></b-table>
  </div>
</template>

<script>
import data from '@/data'
export default {
  name: 'Board',
  data() {
    return {
      fields: [
        {
          key: 'content_id',
          label: '글번호',
        },
        {
          key: 'title',
          label: '제목',
        },
        {
          key: 'user_name',
          label: '글쓴이'
        },
        {
          key: 'created_at',
          label: '등록일'
        }
      ],
      items: data.Content.sort((a,b) => b.content_id-a.content_id).map(contentItem => {
        return {
          ...contentItem,
          user_name: data.User.filter(userItem => userItem.user_id === contentItem.user_id)[0].name
        }
      })
    }
  }
}
</script>