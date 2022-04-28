<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-buttons slot="start">
          <ion-menu-button color="primary"></ion-menu-button>
        </ion-buttons>
        <ion-title>{{ $route.params.id }}</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">{{ $route.params.id }}</ion-title>
        </ion-toolbar>
      </ion-header>

      <div id="container">
        <strong class="capitalize">{{ $route.params.id }}</strong>
        <div
          @mouseover="onMouseOver"
          @mouseleave="onMouseLeave"
          class="hover-div"
        >
          Hover me<br />
          {{ message }}
        </div>
      </div>
      <div ref="tooltipScreen" class="tooltip">Tooltip screen</div>
      <div ref="tooltipPage" class="tooltip">Tooltip page</div>
      <div ref="tooltipClient" class="tooltip">Tooltip client</div>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import {
  IonButtons,
  IonContent,
  IonHeader,
  IonMenuButton,
  IonPage,
  IonTitle,
  IonToolbar,
} from "@ionic/vue";
import { ref, Ref } from "vue";

export default defineComponent({
  name: "FolderPage",
  components: {
    IonButtons,
    IonContent,
    IonHeader,
    IonMenuButton,
    IonPage,
    IonTitle,
    IonToolbar,
  },
  setup() {
    const tooltipScreen: Ref<any> = ref(undefined);
    const tooltipPage: Ref<any> = ref(undefined);
    const tooltipClient: Ref<any> = ref(undefined);
    const message = ref("");
    function onMouseOver(event: any) {
      console.log("onMouseOver", event);
      message.value = `screenX: ${event.screenX}, clientX: ${event.clientX}, pageX: ${event.pageX}`;
      tooltipScreen.value!.style.top = event.screenY + "px";
      tooltipScreen.value!.style.left = event.screenX + "px";

      tooltipPage.value!.style.top = event.pageY + "px";
      tooltipPage.value!.style.left = event.pageX + "px";

      tooltipClient.value!.style.top = event.clientY + "px";
      tooltipClient.value!.style.left = event.clientX + "px";

      tooltipScreen.value!.style.visibility = "visible";
      tooltipPage.value!.style.visibility = "visible";
      tooltipClient.value!.style.visibility = "visible";
    }
    function onMouseLeave(event: any) {
      console.log("onMouseLeave", event);
      message.value = "";
      tooltipScreen.value!.style.visibility = "hidden";
      tooltipPage.value!.style.visibility = "hidden";
      tooltipClient.value!.style.visibility = "hidden";
    }
    return {
      onMouseOver,
      onMouseLeave,
      tooltipScreen,
      tooltipPage,
      tooltipClient,
      message,
    };
  },
});
</script>

<style scoped>
#container {
  text-align: center;
  position: absolute;
  left: 0;
  right: 0;
  top: 50%;
  transform: translateY(-50%);
}

#container strong {
  font-size: 20px;
  line-height: 26px;
}

#container p {
  font-size: 16px;
  line-height: 22px;
  color: #8c8c8c;
  margin: 0;
}

#container a {
  text-decoration: none;
}

.hover-div {
  margin: 15px;
  padding: 15px;
  background: lightblue;
}

.tooltip {
  position: absolute;
  visibility: hidden;
  background: white;
  border: 1px solid #eeeeee;
}
</style>
