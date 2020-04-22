<template>
    <div>


<section class="contact-v3 padding-top-xl">
        <div class="container max-width-xs margin-bottom-lg">
          <div class="text-component text-center">
            <h1>聯絡我們 </h1>
            <p>Lorem ipsum dolor, sit amet consectetur adipisicing elit. Ducimus eos impedit nesciunt voluptates magni vero itaque.</p>
          </div>
        </div>
      
        <div class="container max-width-adaptive-md">
          <div class="grid grid-gap-lg">
            <div class="col-6@md">
              <dl class="details-list-v2 ">
                <div class="details-list-v2__item">
                  <dt class="details-list-v2__dt">油麻地辦公室</dt>
                  <dd class="details-list-v2__dd">
                        彌敦道555號<br>九龍行10樓1001室<br>
                        (油麻地MTR A1 出口)
                  </dd>
                </div>
                <div class="details-list-v2__item">
                        <dt class="details-list-v2__dt">中環辦公室</dt>
                        <dd class="details-list-v2__dd">
                                德輔道中113-125A號<br>
                                遠東發展大廈17樓05室 <br>
                                (中環MTR B 出口)
                              (油麻地MTR A1 出口)
                        </dd>
                      </div>      
                <div class="details-list-v2__item">
                  <dt class="details-list-v2__dt">電郵</dt>
                  <dd class="details-list-v2__dd">
                    <a href='mailto:enquiry@linkedu.hk'>enquiry@linkedu.hk</a>
                  </dd>
                </div>
      
                <div class="details-list-v2__item">
                  <dt class="details-list-v2__dt">電話</dt>
                  <dd class="details-list-v2__dd">
                    <a href='tel:+852 2116 3234'>+852 2116 3234</a> <br><small class='color-contrast-medium'>Mon - Fri, 9AM - 5PM</small>
                  </dd>
                </div>
              </dl>
            </div>
      
            <div class="col-6@md">
              
              <form  @submit.prevent="addContact">
                <div class="margin-bottom-sm">
                  <label class="form-label margin-bottom-xxs" for="contactName">名字</label>
                  <input class="form-control width-100%" type="text" v-model='contactName' name="contactName" id="contactName" required>
                </div>
            
                <div class="margin-bottom-sm">
                  <label class="form-label margin-bottom-xxs" for="contactEmail">電郵</label>
                  <input class="form-control width-100%" type="email" v-model='contactEmail' name="contactEmail" id="contactEmail">
                </div>
                <div class="margin-bottom-sm">
                        <label class="form-label margin-bottom-xxs" for="contactPhone">電話</label>
                        <input class="form-control width-100%" type="text" v-model='contactPhone' name="contactPhone" id="contactPhone">
                      </div>           
                <div class="margin-bottom-sm">
                  <label class="form-label margin-bottom-xxs" for="contactMessage">信息</label>
                  <textarea class="form-control width-100%" rows="9" v-model='contactMessage' name="contactMessage" id="contactMessage"></textarea>
                </div>
              
                <div class="text-right" v-if='!isSubmit'>
                  <button class="btn btn--primary" type="submit">提交</button>
                </div>
                <h3 class="margin-bottom-sm" v-if='isSubmit'>謝謝你的提交！我們會盡快聯絡你！</h3>
              </form>
            </div>
          </div>
        </div>
      
        <div role="application" class="google-maps google-maps--ratio-3:1 margin-top-lg js-google-maps" data-coordinates="51.5658015,-0.40339"><!-- Google Map --></div>
      </section>


    </div>
</template>

<script>
export default {
  data() {
    return {
      contactName: '',
      contactEmail: '',
      contactPhone: '',
      contactMessage: '',
      isSubmit : false
    }
  },
  head() {
    return {
      script: [
        { src: 'https://maps.googleapis.com/maps/api/js?key=AIzaSyAwutFTptdqFWUYqkbIplagTm1aYqzDArc&callback=initGoogleMap' , defer: true, body: true } 
      ]
    }
  },
  methods: {
    async addContact() {
      await this.$axios.$post('http://whostsite.com/contacts',{
        name: this.contactName,
        email: this.contactEmail,
        phone: this.contactPhone,
        message: this.contactMessage,
        securitytoken: 'ds%sdfj3asfaf%d'
      })
      .then((response) => {
        console.log(response)
        this.isSubmit = true
      })
      .catch((response) => {
        console.log(response)
      })
    }
  }
}

</script>