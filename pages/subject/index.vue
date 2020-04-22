<template>
    <div>
             <section class="home-popular-subjects othersubject" style="padding-top:5em;">
                   
                    <div class="container">
                      <div class="grid justify-center">
                        <div class="col-10">
                        <div class="container max-width-adaptive-sm">
                            <h2 class="margin-bottom-sm">熱門科目</h2>
                            <p class="margin-bottom-lg">Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</p>
                            
                            <div class="author bg-contrast-lower padding-md margin-top-md margin-bottom-xl">

                                    <a href="#0" class="author__img-wrapper">
                                      <img src="/img/maisie.png" alt="Author picture">
                                    </a>
                              
                                    <div class="author__content text-component v-space-xxs">
                                      <h4 class="">升學顧問 - Maisie</h4>
                                      <p class="padding-top-sm color-contrast-medium text-sm">英國中學為7年制，3年初中，然後修讀2年GCSE。之後修讀2年的高中科程，同學可選擇GCE A-Level、International Baccalaureate (IB) 或BTEC。 不同課程適合不同學生，大部分學校設有入學試，包括筆試及面試，我們會為學生安排入學試的事宜。</p>
                                     
                                    </div>

                                    
                            </div>
                        </div>
                         
                        
                         
                        </div>
                      </div>

                      <subjects :subjectobject="articles"/>
                    </div>
                  </section>

    </div>
</template>

<script>
import subjects from '~/components/subjects'
export default {
  components:{
    subjects
  },
  data(){
    return{
       backendurl : process.env.backendurl,
       frontendurl : process.env.frontendurl,
    }
  },
  async asyncData({ $axios }) {
    const articles = await $axios.$get(process.env.backendurl+'subjects')
    return { articles }
  },
}

</script>
