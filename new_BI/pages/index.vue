<template>
  <div class="dashboard-container">
    <component :is="currentRole"/>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
import adminDashboard from '@/components/Dashboard/admin'
import editorDashboard from '@/components/Dashboard/editor'

export default {
  name: 'Dashboard',
  components: { adminDashboard, editorDashboard },
  data() {
    return {
      currentRole: 'adminDashboard'
    }
  },
  computed: {
    ...mapGetters([
      'roles'
    ])
  },
  created() {

  },
  //在页面加载到浏览器前调用 服务端渲染
  async asyncData({$axios}){
    let data = await $axios.$get("/test",{progress:false});
    return {status:data}
  },
  //页面ajax;
  mounted(){
    this.$axios.$get("/test",{progress:false})
    .then(res =>{
      console.log(res);
    })
  }
}
</script>
