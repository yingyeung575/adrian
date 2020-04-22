<template>
    <div>
           <section >
            <article class="padding-y-xl">
                    <header class="container max-width-xs margin-bottom-lg">
                      <div class="text-component text-center line-height-lg v-space-md margin-bottom-md">
                        <h1>{{ article.title }}</h1>
                        <p v-if="article.excerpt" class="color-contrast-medium text-md">{{ article.excerpt }}</p>
                            <div class="margin-bottom-xs">
                              <a v-for='(category,idx) in article.categories' v-bind:key='idx' :href="frontendurl + 'category/' + category.slug" class="story__category">
                                <i>{{ category.name }}</i>
                              </a>
                             
                            </div>
                      </div>
                  
                      <div class="flex justify-center">
                        <div class="author author--meta">
                          <a href="#0" class="author__img-wrapper">
                            <img v-if='article.author' :src="backendurl + article.author.profile.url">
                          </a>
                  
                          <div class="author__content text-component v-space-xxs">
                            <h4 v-if='article.author' class="text-base"><span rel="author">{{ article.author.name }}</span></h4>
                            <p class="text-sm color-contrast-medium"><time>{{ article.date }}</time></p>
                                                   
                          </div>
                        </div>
                      </div>
                    </header>
                  
                    <figure class="container max-width-adaptive-sm margin-bottom-lg">
                       <img v-if='article.thumbnail' :src="backendurl + article.thumbnail.url">
                    </figure>
                  
                    <div class="container max-width-adaptive-sm">
                      <div class="text-component line-height-lg v-space-md">

                        <div v-bind:key='idy' v-for='(content, idy) in article.maincontent'>
                          <div v-if="content.text" v-html="$md.render(content.text)"> </div> 
                          <div class='tableofcontent' v-if="content.tableofcontent" v-html="$md.render(content.tableofcontent)"> </div> 
                          <div class="text-component__block text-component__block--outset" v-if="content.html" >
                            <figure class="media-wrapper" v-if="content.html" v-html="content.html">
                            
                            </figure>
                          </div>
                          <figure class="text-component__block" v-if="content.__component === 'image.image'">
                             <a v-if='content.link' :href='content.link'>
                                <img :src="backendurl + content.image.url">
                             </a>
                             <img v-if='!content.link' :src="backendurl + content.image.url">
                            <figcaption>{{ content.caption }}</figcaption>
                          </figure>
                    
                        </div>
                     
                      </div>
                    </div>
                  </article>
     </section>
            

     <section class="padding-y-xl bg-contrast-lower">
            <div class="container max-width-adaptive-lg">
              <div class="margin-bottom-md">
                <h3 class="text-md">你可能也會喜歡...</h3>
              </div>
            
              <div class="grid grid-gap-md">
                <article class="story-v2 col-6@md col-4@xl">
                  <div class="story-v2__meta">
                    <p> <span role="separator"></span> <time datetime="2020-05-20">May 20, 2020</time> </p>
                  </div>
          
                  <div class="text-component">
                    <h2 class="story-v2__headline"><a href="#0">Lorem ipsum dolor sit amet consectetur</a></h2>
                    <p class="story-v2__excerpt">Lorem ipsum dolor sit amet, consectetur adipisicing elit. Iusto saepe voluptate similique vel et nihil numquam.</p>
                  </div>
                </article>
            
                <article class="story-v2 col-6@md col-4@xl">
                        <div class="story-v2__meta">
                          <p> <span role="separator"></span> <time datetime="2020-05-20">May 20, 2020</time> </p>
                        </div>
                
                        <div class="text-component">
                          <h2 class="story-v2__headline"><a href="#0">Lorem ipsum dolor sit amet consectetur</a></h2>
                          <p class="story-v2__excerpt">Lorem ipsum dolor sit amet, consectetur adipisicing elit. Iusto saepe voluptate similique vel et nihil numquam.</p>
                        </div>
                      </article>
              </div>
            </div>
          </section>

    </div>
</template>
<script>  
export default {  
  data(){
    return{
       backendurl : process.env.backendurl,
       frontendurl : process.env.frontendurl,
   

    }
  },
  async asyncData({ $axios, params }) {
    const articles = await $axios.$get(process.env.backendurl+'articles?slug='+params.slug)
    
    let article = articles[0];
    return { article }
  },



}
</script> 
