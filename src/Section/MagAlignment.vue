<template>
  <div>
    <div>
      <ModelCanvas :gps-pitch-axis="pitchAxis" :gps-roll-axis="rollAxis" :gps-yaw-axis="yawAxis"></ModelCanvas>
    </div>
    <div>
      <p>Moves the axis to rotate the GPS module</p>
      <div>
        <b>Pitch Axis:
          <el-button type="primary" size="mini" v-on:click="resetRollAxis">Reset</el-button>
        </b>
        <div>
          <el-slider v-model="rollAxis" :min="-180" :max="180" :marks="{'-180':'-180°','180':'180°'}" show-input/>
        </div>
      </div>
      <div class="mt-2">
        <b> Roll Axis:
          <el-button type="primary" size="mini" v-on:click="resetPitchAxis">Reset</el-button>
        </b>
        <el-slider v-model="pitchAxis" :min="-180" :max="180" :marks="{'-180':'-180°','180':'180°'}" show-input/>
      </div>
      <div>
        <b> Yaw Axis:
          <el-button type="primary" size="mini" v-on:click="resetYawAxis">Reset</el-button>
        </b>
        <el-slider v-model="yawAxis" :min="-360" :max="360" :step="45" :marks="{'-360':'-360°','360':'360°'}"
                   show-input show-stops/>
      </div>
    </div>
    <div :style="{margin:'30px'}">
      <el-card :body-style="{padding:'5px'}">
        <template #header><b>INav CLI commands</b></template>
        <p>Copy and paste this lines on CLI in INav Configurator</p>
        <p>
          set align_mag_roll = {{ Number(rollAxis) * 10 }}<br>
          set align_mag_pitch = {{ (180 - Number(pitchAxis)) * 10 }}<br>
          set align_mag_yaw = {{ (270 + Number(yawAxis)) * 10 }}
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
  yaw: 0
}

export default {
  name: "MagAlignment",
  components: {ModelCanvas},
  data() {
    return {
      rollAxis: 0,
      pitchAxis: 0,
      yawAxis: 0,
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
    }
  }
}
</script>

<style scoped>
.slider {
  width: 100%;
}
</style>