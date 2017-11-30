<template>
  <div class="hello">
    <h1>AWS Fargate Pricing Calculator</h1>
    <el-select v-model="time" placeholder="Select" @change="handleTimeFormatChange">
      <el-option
        v-for="item in timeOptions"
        :key="item.value"
        :label="item.label"
        :value="item.value"
        >
      </el-option>
    </el-select>

    <div v-if="time === 'hours'" style="display: inline">
      x 
      <el-input-number v-model="hours" controls-position="right" :min="1" :max="730"></el-input-number>
    </div>

    x

    <el-select v-model="vcpu" placeholder="Select">
      <el-option
        v-for="item in vcpuOptions"
        :key="item.value"
        :label="item.label"
        :value="item.value">
      </el-option>
    </el-select>

    x

    <el-select v-model="memory" placeholder="Select">
      <el-option
        v-for="item in memoryOptions"
        :key="item.value"
        :label="item.label"
        :value="item.value">
      </el-option>
    </el-select>

    =

    <h2>${{ totalPrice }}/month</h2>
  </div>
</template>

<script>
const vcpuHourPrice = 0.0506;
const memoryGbHourPrice = 0.0127;

const mapSequenceToSelections = array => array.map(x => ({
  value: x,
  label: `${x}GB`,
}));

const getMemoryOptions = (vcpu) => {
  if (vcpu === 0.25) {
    return mapSequenceToSelections([0.5, 1, 2]);
  } else if (vcpu === 0.5) {
    return mapSequenceToSelections([1, 2, 3]);
  } else if (vcpu === 1) {
    return mapSequenceToSelections([...Array(7).keys()].map(x => x + 2));
  } else if (vcpu === 2) {
    return mapSequenceToSelections([...Array(13).keys()].map(x => x + 4));
  }

  return mapSequenceToSelections([...Array(23).keys()].map(x => x + 8));
};

export default {
  name: 'Calculator',
  data() {
    return {
      vcpuOptions: [{
        value: 0.25,
        label: '0.25 vCPU',
      }, {
        value: 0.5,
        label: '0.5 vCPU',
      }, {
        value: 1,
        label: '1 vCPU',
      }, {
        value: 2,
        label: '2 vCPU',
      }, {
        value: 4,
        label: '4 vCPU',
      }],
      timeOptions: [{
        value: 'hours',
        label: 'Hours',
      }, {
        value: 'month',
        label: 'Whole Month (730hrs)',
      }],
      vcpu: 0.25,
      memory: 0.5,
      time: 'hours',
      hours: 1,
    };
  },
  computed: {
    memoryOptions: function() { // eslint-disable-line
      return getMemoryOptions(this.vcpu);
    },
    totalPrice: function() { // eslint-disable-line
      return (this.hours * this.vcpu * vcpuHourPrice)
        + (this.hours * this.memory * memoryGbHourPrice);
    },
  },
  methods: {
    handleTimeFormatChange: function (event) { // eslint-disable-line
      if (event === 'month') {
        this.hours = 730;
      } else {
        this.hours = 1;
      }
    },
  },
};
</script>

<style scoped>
</style>
