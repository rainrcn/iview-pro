<template lang="html">
    <div id="mountNode"></div>
</template>

<script>
import G2 from '@antv/g2';
import DataSet from '@antv/data-set';

export default {
  // name:"基础折线图",
  data() {
    return {
      data: [{
        item: '事例一',
        count: 40
      }, {
        item: '事例二',
        count: 21
      }, {
        item: '事例三',
        count: 17
      }, {
        item: '事例四',
        count: 13
      }, {
        item: '事例五',
        count: 9
      }],
    }
  },
  methods: {
    creatChart(data) {
      var _DataSet = DataSet,
        DataView = _DataSet.DataView;
      var dv = new DataView();
      dv.source(data).transform({
        type: 'percent',
        field: 'count',
        dimension: 'item',
        as: 'percent'
      });
      var chart = new G2.Chart({
        container: 'mountNode',
        padding: [20, 20, 60, 20],
        forceFit: true,
        height: 400
      });
      chart.source(dv, {
        percent: {
          formatter: function formatter(val) {
            val = val * 100 + '%';
            return val;
          }
        }
      });
      chart.coord('theta', {
        radius: 0.75
      });
      chart.tooltip({
        showTitle: false,
        itemTpl: '<li><span style="background-color:{color};" class="g2-tooltip-marker"></span>{name}: {value}</li>'
      });
      chart.intervalStack().position('percent').color('item').label('percent', {
        formatter: function formatter(val, item) {
          return item.point.item + ': ' + val;
        }
      }).tooltip('item*percent', function(item, percent) {
        percent = percent * 100 + '%';
        return {
          name: item,
          value: percent
        };
      }).style({
        lineWidth: 1,
        stroke: '#fff'
      });
      chart.render();
    }
  },
  mounted() {
    this.$nextTick(() => {
      this.creatChart(this.data)
    })
  }
}
</script>

<style lang="css">
</style>
