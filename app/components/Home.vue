<template>
  <Page class="page">
    <ActionBar class="ab">
      <Label text="Calendar" class="header"/>
    </ActionBar>
    
    <FlexboxLayout flexDirection="column">
      
      <GridLayout rows="auto" columns="*, *, *">
        <Image col="0" src="~/assets/previous.png" width="35%" stretch="aspectFit" class="button"/>
        <Image col="1" src="~/assets/home.png" width="20%" stretch="aspectFit" class="button"/>
        <Image col="2" src="~/assets/next.png" width="35%" stretch="aspectFit" class="button"/>
      </GridLayout>
    </FlexboxLayout>
  </Page>
</template>

<script>
export default {
  data () {
    return {};
  },
  methods: {}
};
</script>

<style scoped lang="scss">

</style>
