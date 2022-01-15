<template>
  <el-row :glutter="24" justify="center" align="middle" >
      <el-col :span="6">
        3D Models by
        <el-link href="https://grabcad.com/library/beitian-bn-880-gps-and-compas-module-1" target="_blank">Morten
          Nielsen
        </el-link>
        and
        <el-link href="https://github.com/iNavFlight/inav-configurator" target="_blank">INAV Configurator</el-link>
      </el-col>
      <el-col :span="4">
        Developed by
        <el-link href="https://www.youtube.com/channel/UCQgDwlProz9y8DsF1lFjAhQ" target="_blank">Luca Giovannesi
        </el-link>
      </el-col>
      <el-col :span="5">
        <el-row :glutter="9" justify="center" align="middle">
          <el-col :span="8">Buy me a coffee</el-col>
          <el-col :span="1">
            <a href="https://www.paypal.com/paypalme/LucaGiovannesi" target="_blank">
              <img alt="Donate button" src="https://www.paypalobjects.com/en_US/i/btn/btn_donate_LG.gif"/>
            </a>
          </el-col>
        </el-row>
      </el-col>
  </el-row>
</template>

<script>

export default {
  name: "Footer",
  components: {}
}
</script>

<style scoped>

</style>