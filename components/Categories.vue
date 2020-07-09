<template>
  <div class="topcontainer" :style="`backgroundImage: url('${indexCvCategory.image[0].url}')`">

    <!-- nav bar -->
    <nav class="navbar navbar-fixed-top">
        <div class="container">
            <div class="navbar-header">
                <a class="navbar-brand" href="#top">
                    Grégory DAY
                </a>
                <!-- bouton "hamburger" (visible uniquement sur mobile) -->
                <button class="navbar-toggle collapsed" data-toggle="collapse" data-target="#menu">
                    <i class="fa fa-bars fa-1x"></i>
                </button>
            </div>
            
            <div class="navbar-collapse collapse" id="menu">
                <ul 
                class="nav navbar-nav navbar-right"
                v-for="category in cvCategories.slice().reverse()"
                :key="category.id"   
                >
                    <li><a :href="`#rubrique${category.id}`">{{ category.title }}</a></li>
                </ul>
            </div>
        </div>
    </nav>



    <!-- header -->
    <header 
        class="container containjumbo text-center" 
        id="top"
    >
        <div class="row">
            <div class="col-xs-1 hidden-sm hidden-md hidden-lg"></div>
            <div class="jumbotron col-xs-10 col-sm-12 col-md-12 col-lg-12">
                <figure class="col-md-offset-5 col-md-2 col-sm-offset-5 col-sm-2 col-xs-offset-4 col-xs-4">
                    <img :src="indexCvCategory.articles[0].image.url" alt="" class="img-responsive"/>
                </figure>
                <h1 class="col-md-offset-3 col-md-6 col-sm-offset-2 col-sm-8 col-xs-12">{{ indexCvCategory.articles[0].title }}</h1> 
                <p class="col-md-offset-4 col-md-4 col-sm-offset-3 col-sm-6 col-xs-12">{{ indexCvCategory.articles[0].subtitle }},<br>{{ indexCvCategory.articles[0].content }}</p> 
            </div>
            <div class="col-xs-1 hidden-sm hidden-md hidden-lg"></div>
        </div>
    </header>




    <!-- rubriques -->
    <div
        v-for="category in cvCategories"
        :key="category.id"    
        :class="`container${category.id} rubrique${category.id} text-center`" 
        :id="`rubrique${category.id}`"
        :style="`backgroundImage: url('${category.image[0] ? category.image[0].url : ''}')`"
    >
        <div class="row">
            <div :class="`col-md-12 ${category.image[0] ? 'quiEspaceImage' : 'quiEspace'} text-uppercase`">
                <h2>{{ category.title }}</h2>      
                <p>{{ category.subtitle }}</p> 
                <p><b>______</b></p> 
            </div>
            <div v-if="category.id == 4 || category.id == 6">
                <div 
                    class="col-xs-offset-1 col-xs-10 col-sm-offset-2 col-sm-8 col-md-offset-2 col-md-8"
                    v-for="article in category.articles.reverse()"
                    :key="article.id"
                >
                    <div class="media">
                        <div class="media-left">
                            <img :src="`${article.image ? article.image.url : ''}`" alt="" class="img-responsive"/>
                        </div>
                        <div class="media-body text-left">
							<h4 class="media-heading">{{ article.title }}</h4>
							<p>{{ article.subtitle }}</p>
							<p>{{ article.content }}</p>
                        </div>
                    </div>
                    <div class="col-xs-1 col-sm-2 col-md-2"></div>
				    <div class="col-xs-12 col-sm-12 col-md-12 quiEspace2"></div>
                </div>
            </div>		
            <div v-else>
                <div 
                    class="col-md-4"
                    v-for="article in category.articles"
                    :key="article.id"
                >
                    <div class="thumbnail">
                        <i v-bind:class="`${article.icon_class}`" style="font-size:4em"></i>
                        <div :class="`${!category.image[0] ? 'captiontextonwhite' : 'caption'}`">
                            <h3>{{ article.title }}</h3>
                            <p>{{ article.subtitle }}</p>
                            <p>{{ article.content }}</p>
                        </div>
                    </div>
                </div>
            </div>			
        </div>
    </div>





    <!-- footer -->
    <footer class="nb-footer">
        <div class="container">
            <div class="row">
                <div class="col-sm-12">
                    <p><a :href="`mailto:${footerCvCategory.articles[0] ? footerCvCategory.articles[0].subtitle : ''}`">{{ footerCvCategory.articles[0] ? footerCvCategory.articles[0].subtitle : '' }}</a></p>
                </div>
                <div class="col-sm-12">
                    <div class="about">
                        <div class="social-media">
                            <ul class="list-inline">
                                <li><a :href="`${footerCvCategory.articles[1] ? footerCvCategory.articles[1].subtitle : ''}`" target="_blank" title=""><i v-bind:class="`${footerCvCategory.articles[1] ? footerCvCategory.articles[1].icon_class : ''}`"></i></a></li>
                                <li><a :href="`${footerCvCategory.articles[2] ? footerCvCategory.articles[2].subtitle : ''}`" target="_blank" title=""><i v-bind:class="`${footerCvCategory.articles[2] ? footerCvCategory.articles[2].icon_class : ''}`"></i></a></li>
                            </ul>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <div class="copyright">
            <div class="container">
                <div class="row">
                    <div class="text-center">
                        <p>Grégory Day 2020</p>
                    </div>
                    <div class="col-sm-6"></div>
                </div>
            </div>
        </div>
    </footer>


  </div>
</template>

<script>
export default {
  data: function() {
    return {
      api_url: process.env.strapiBaseUri
    };
  },
  props: {
    categories: Array
  },
  computed: {
    countCategories() {
        return this.categories.length;
    },
    indexCvCategory() {
        return this.categories.sort(function (a, b) {
            return a.id - b.id;
        }).slice(0, 1)[0];
    },
    footerCvCategory() {
        return this.categories.sort(function (a, b) {
            return a.id - b.id;
        }).slice(this.categories.length -1, this.categories.length)[0];
    },
    cvCategories() {
        return this.categories.sort(function (a, b) {
            return a.id - b.id;
        }).slice(1, this.categories.length -1)
    }
  }
};
</script>