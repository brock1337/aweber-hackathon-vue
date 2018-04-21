<template>
  <div>
    <container>
      <row class="mt-5">
        <column sm="4">
          <card>
            <card-img src="https://mdbootstrap.com/img/Photos/Horizontal/Nature/4-col/img%20%282%29.jpg" alt="Card image cap" waves></card-img>
            <card-body>
              <card-title>Card with waves effect</card-title>
              <card-text>Some quick example text to build on the card title and make up the bulk of the card's content.</card-text>
              <btn color="primary">Button</btn>
            </card-body>
          </card>
        </column>
        <column sm="4">
          <card>
            <card-img src="https://mdbootstrap.com/img/Photos/Horizontal/Nature/4-col/img%20%286%29.jpg" alt="Card image cap"></card-img>
            <card-body>
              <card-title>Basic card</card-title>
              <card-text>Some quick example text to build on the card title and make up the bulk of the card's content.</card-text>
              <btn color="primary">Button</btn>
            </card-body>
          </card>
        </column>
        <column sm="4">
          <card>
            <card-img src="https://mdbootstrap.com/img/Photos/Horizontal/Nature/4-col/img%20%287%29.jpg" alt="Card image cap" waves></card-img>
            <card-body>
              <card-title>Card with waves effect</card-title>
              <card-text>Some quick example text to build on the card title and make up the bulk of the card's content.</card-text>
              <btn color="primary">Button</btn>
            </card-body>
          </card>
        </column>
      </row>
    </container>
    
    
    <div class="">
      <button @click="enableNotifications" class="">
        Enable Notifications
      </button>
    </div>
  
  </div>
</template>

<script>
  import axios from 'axios';

  import Btn from '@/components/Button';
  import Container from '@/components/Container';
  import Row from '@/components/Row';
  import Column from '@/components/Col';
  import Card from '@/components/Card';
  import CardImg from '@/components/CardImg';
  import CardHeader from '@/components/CardHeader';
  import CardBody from '@/components/CardBody';
  import CardTitle from '@/components/CardTitle';
  import CardText from '@/components/CardText';
  
  
  export default {
    name: "HomePage",
    components: {
      Btn,
      Container,
      Column,
      Row,
      Card,
      CardImg,
      CardBody,
      CardHeader,
      CardTitle,
      CardText
    },
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
            
            axios.post(
              'http://127.0.0.1:3000/subscribe',
              {
                email: 'ricanontherun@gmail.com',
                tags: ['national_security'],
                headers: {
                  'Allow-Control-Access-Origin': '*'
                }
              },
              
            )
            .then(result => {
              console.log('[API Subscribers]: ', result);
            })
            .catch(error => {
              console.error('[ERROR]: ', error);
            });
            
          });
        }
      }
    }
  }
</script>

<style scoped>

</style>
