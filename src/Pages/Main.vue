<template>
  <el-container>
    <el-header>
      <el-row :gutter="24" align="middle" justify="space-between">
        <el-col :span="18" align="left">
          <h2>INav magnetometer alignment helper</h2>
        </el-col>
        <el-col :span="4" align="right">
          <!-- Place this tag where you want the button to render. -->
          <a class="github-button" href="https://github.com/kernel-machine/INavMagAlignHelper" data-size="large"
             aria-label="View on GitHub">View on GitHub</a>
        </el-col>
      </el-row>
    </el-header>
    <el-main>
      <MagAlignment/>
    </el-main>
    <el-footer>
      <Footer class="mt-5"/>
    </el-footer>
  </el-container>
</template>

<script>
import Footer from "@/components/Footer";
import MagAlignment from "@/Section/MagAlignment";

export default {
  name: "Main",
  components: {MagAlignment, Footer}
}
</script>

<style scoped>


</style>