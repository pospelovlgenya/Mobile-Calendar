<template>
  <Page class="page">
    <ActionBar class="ab">
      <Label text="Calendar" class="header"/>
    </ActionBar>
    
    <FlexboxLayout flexDirection="column">
      <GridLayout rows="auto" columns="*, 3*, *">
        <Label col="0" :text="StrMonthP" textWrap="true" class="button"/>
        <Label col="1" :text="StrMonthD" textWrap="true" class="button"/>
        <Label col="2" :text="StrMonthN" textWrap="true" class="button"/>
      </GridLayout>
      

      <GridLayout rows="auto" columns="*, *, *">
        <Image col="0" src="~/assets/previous.png" width="35%" stretch="aspectFit" @tap="selectedMonth--" class="button"/>
        <Image col="1" src="~/assets/home.png" width="20%" stretch="aspectFit" @tap="selectedMonth = 0" class="button"/>
        <Image col="2" src="~/assets/next.png" width="35%" stretch="aspectFit" @tap="selectedMonth++" class="button"/>
      </GridLayout>
    </FlexboxLayout>
  </Page>
</template>

<script>
export default {
  data () {
    return {
      selectedMonth: 0,
      show: 0,
      nowDay: this.getNowDay(),
      StrMonthP: '',
      StrMonthD: '',
      StrMonthN: '',
    };
  },
  beforeMount() {
    this.getShow();
  },
  watch: {
    selectedMonth: function() {
      this.getShow();
    },
  },
  methods: {
    getShow() {
      var base = new Date();

      var p = new Date(base.getFullYear(), base.getMonth() + this.selectedMonth - 1, 1);
      var t = new Date(base.getFullYear(), base.getMonth() + this.selectedMonth, 1);
      var n = new Date(base.getFullYear(), base.getMonth() + this.selectedMonth + 1, 1);
      this.StrMonthP = p.getFullYear() + ' ' + p.toDateString().slice(4, 7);
      this.StrMonthD = t.getFullYear() + ' ' + t.toDateString().slice(4, 7);
      this.StrMonthN = n.getFullYear() + ' ' + n.toDateString().slice(4, 7);

      var day = t.getDay();
      if (day == 0) {
        day = 6;
      }
      else {
        day--;
      }

      // this.show

    },
    getNowDay() {
      var a = new Date();
      return new Date(a.getFullYear(), a.getMonth(), a.getDate());
    },
  }
};
</script>

<style scoped lang="scss">

</style>
