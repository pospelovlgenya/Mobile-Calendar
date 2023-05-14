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

      <GridLayout rows="auto" columns="*, *, *, *, *, *, *" class="name-day">
          <Label col="0" text="Mo" textWrap="true" />
          <Label col="1" text="Tu" textWrap="true" />
          <Label col="2" text="We" textWrap="true" />
          <Label col="3" text="Th" textWrap="true" />
          <Label col="4" text="Fr" textWrap="true" />
          <Label col="5" text="Sa" textWrap="true" />
          <Label col="6" text="Su" textWrap="true" />
      </GridLayout>
      <GridLayout rows="auto, auto, auto, auto, auto, auto, auto" columns="*" v-for="(week, index) in show" :key="index">
        <GridLayout :row="index + 1" rows="auto" columns="*, *, *, *, *, *, *" v-for="(day, idx) in week" :key="idx">
              <Label :col="idx" :text="day.day" textWrap="true" class="month-day" v-if="day.state == 'thisMonth'"/>
              <Label :col="idx" :text="day.day" textWrap="true" class="today" v-else-if="day.state == 'thisDay'"/>
              <Label :col="idx" :text="day.day" textWrap="true" class="notMonth-day" v-else/>
          </GridLayout>
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
      show: [],
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
      const nowDay = new Date(base.getFullYear(), base.getMonth(), base.getDate());

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

      var v = new Date(t.getFullYear(), t.getMonth(), t.getDate() - day);
      this.show = [];
      var state = 'notThis';
      for (var i = 0; i < 6; i++)
      {
        this.show.push([]);
        for (var j = 0; j < 7; j++) {
          state = 'notThis';
          if (v.getMonth() == t.getMonth()) {
            state = 'thisMonth';
          }
          if (v.getMonth() == nowDay.getMonth() && v.getDate() == nowDay.getDate()) {
            state = 'thisDay';
          }
          this.show[i].push({day: v.getDate(), state: state});
          v.setDate(v.getDate() + 1);
        }
      }
    },
  }
};
</script>

<style scoped lang="scss">

</style>
