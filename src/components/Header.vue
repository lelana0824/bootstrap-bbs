<template>
  <div>
    <b-navbar toggleable="lg" type="dark" variant="info">
      <b-navbar-brand href="#">Vue.js로 게시판 만들기</b-navbar-brand>

      <b-navbar-toggle target="nav_collapse"/>

      <b-collapse is-nav id="nav_collapse">
        <b-navbar-nav>
          <b-nav-item href="#">공지사항</b-nav-item>
          <b-nav-item href="#">자유게시판</b-nav-item>
          <b-nav-item href="#">구인구직</b-nav-item>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </div>
</template>

<script>
export default {
  name: "Header",
  data() {
    return {};
  }
};
</script>

