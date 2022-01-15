<template>
  <div>
    <div>
      <ModelCanvas :gps-pitch-axis="pitchAxis" :gps-roll-axis="rollAxis" :gps-yaw-axis="-90-yawAxis"></ModelCanvas>
    </div>
    <div>
      <p>Moves the axes to rotate the GPS module along the quadcopter axes</p>
      <div>
        <b>Pitch Axis:
          <el-button type="primary" size="mini" v-on:click="resetRollAxis">Reset</el-button>
        </b>
        <div>
          <el-slider v-model="rollAxis" :min="-180" :max="180" :marks="generateLabels(-180,180,45)" show-input/>
        </div>
      </div>
      <div class="mt-2">
        <b> Roll Axis:
          <el-button type="primary" size="mini" v-on:click="resetPitchAxis">Reset</el-button>
        </b>
        <el-slider v-model="pitchAxis" :min="-180" :max="180" :marks="generateLabels(-180,180,45)" show-input/>
      </div>
      <div>
        <b> Yaw Axis:
          <el-button type="primary" size="mini" v-on:click="resetYawAxis">Reset</el-button>
        </b>
        <el-slider v-model="yawAxis" :min="-180" :max="360" :step="45" :marks="generateLabels(-180,360,45)"
                   show-input show-stops/>
      </div>
    </div>
    <div :style="{margin:'30px'}">
      <el-card :body-style="{padding:'5px'}">
        <template #header><b>INAV CLI commands</b></template>
        <p>Copy and paste this lines on CLI in INAV Configurator</p>
        <p>
          set align_mag_roll = {{ Number(rollAxis) * 10 }}<br>
          set align_mag_pitch = {{ (180 + Number(pitchAxis)) * 10 }}<br>
          set align_mag_yaw = {{ (Number(yawAxis)) * 10 }}
        </p>
        <p>Remember to enter <b>save</b> to save the configuration</p>
      </el-card>
    </div>
  </div>
</template>

<script>
import ModelCanvas from "@/components/ModelCanvas";

const default_value = {
  roll: 0,
  pitch: 0,
  yaw: 270
}

export default {
  name: "MagAlignment",
  components: {ModelCanvas},
  data() {
    return {
      rollAxis: default_value.roll,
      pitchAxis: default_value.pitch,
      yawAxis: default_value.yaw,
    }
  },
  methods: {
    resetRollAxis() {
      this.rollAxis = default_value.roll
    },
    resetPitchAxis() {
      this.pitchAxis = default_value.pitch
    },
    resetYawAxis() {
      this.yawAxis = default_value.yaw
    },
    generateLabels(min, max, interval) {
      let res = []
      for (var i = min; i <= max; i += interval) {
        res[String(i)] = String(i) + "°"
      }
      return res;
    }
  }
}
</script>

<style scoped>
.slider {
  width: 100%;
}
</style>