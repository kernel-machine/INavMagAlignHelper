<template>
  <el-container>
    <el-header>
      <h2>INav magnetometer alignment helper</h2>
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