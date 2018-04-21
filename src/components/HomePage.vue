<template>
  <div>
    <h1>
      Home
    </h1>
    
    <div class="">
      <button @click="enableNotifications" class="">
        Enable Notifications
      </button>
    </div>
  
  </div>
</template>

<script>
  export default {
    name: "HomePage",
    methods: {
      enableNotifications () {
        if ('Notification' in window) {
          Notification.requestPermission(result => {
            console.log('Notification Permission: ', result);
          
            if (result !== 'granted') {
              console.log('No Notification permission granted');
            } else {
              this.displayConfirmNotification();
            }
          });
        } else {
          console.log('Notification was not found in window');
        }
      },
      displayConfirmNotification () {
        if ('serviceWorker' in navigator) {
          console.log('[Service Worker]: in navigator on HomePage');
  
          let options = {
            body: `Breaking News! Now you won't miss any!`,
            icon: '../../static/img/icons/8w-globe-color-96x96.png',
            dir: 'ltr',
            lang: 'en-US'
          };
          
          const notification = new Notification('Successfully subscribed!', options);
  
          notification.addEventListener('click', function(event) {
            console.log('[Service Worker] Notification click Received.', event);
    
            notification.close();
    
            // notification.waitUntil(
            //   self.clients.openWindow('https://developers.google.com/web/')
            // );
          });
        }
      }
    }
  }
</script>

<style scoped>

</style>
