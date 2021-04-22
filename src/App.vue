<template>
  <root>
    <app-navigation></app-navigation>
  </root>
</template>

<script>
import {
  createAppContainer,
  createStackNavigator,
  createDrawerNavigator
} from "vue-native-router";
import { Root } from "native-base";
import SideBarScreen from "./screens/sidebar/index.vue";
import CoinseaScreen from "./screens/coinsea/index.vue";

const Drawer = createDrawerNavigator(
  {
    Coinsea: { screen: CoinseaScreen },
  },
  {
    initialRouteName: "Coinsea",
    contentOptions: {
      activeTintColor: "#aaeeff"
    },
    contentComponent: SideBarScreen
  }
);

const AppNavigation = createAppContainer(
  createStackNavigator(
    {
      Drawer: { screen: Drawer },
    },
    {
      initialRouteName: "Drawer",
      headerMode: "none"
    }
  )
);
export default {
  components: { Root, AppNavigation }
};
</script>
