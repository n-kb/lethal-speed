<template>
  <div >
    <navbar></navbar>
    <section class="section">
      <div class="container is-fluid">
        <div class="columns">
          <div class="column is-2 is-offset-10">
            <shareitem :title="$t('title')" :shareText="$t('share')" :description="$t('lede')"></shareitem>
          </div>
        </div>
        <div class="columns">
          <div class="column is-half is-offset-one-quarter">
            <div class="content">
              <h1 class="title is-1 has-text-centered is-size-3-mobile">{{ $t('title') }}</h1>
              <div class="columns">
                <div class="column has-text-centered">
                  <p>
                    <a v-if="$i18n.locale == 'en'" @click="changeLocale('de')">Auf Deutsch lesen: Tödliche Geschwindlichkeit</a>
                    <a v-if="$i18n.locale == 'de'" @click="changeLocale('en')">Read in English: What's your lethal speed?</a>
                  </p>
                </div>
              </div>
              <div class="columns">
                <div class="column has-text-centered">
                  <p class="byline">{{ $t("An essay by") }} <strong><a href="https://blog.nkb.fr" class="byline--link">Nicolas Kayser-Bril</a></strong></p>
                </div>
                <div class="column byline has-text-centered">
                  <p class="byline">{{ $t("date") }}</p>
                </div>
              </div>
              <div class="article-content">
                <p>
                  I recently published a piece, <a href="http://blog.nkb.fr/license-to-kill/" target="_blank">Licence to Kill</a>, showing how little car and truck drivers had to fear from the Berlin judicial system when they killed someone. Several commenters pointed out that car drivers did not <em>kill</em>. They had <em>accidents</em>.
                </p>
                <p>
                  To illustrate the fault with such thinking, I created the tool below that lets you calculate the speed over which you put others in danger.
                </p>
                <calculator @callback="updateVars"/>
                <p>
                  A {{ vehicle.type }} weighting {{ total_weight }} (in total) traveling at {{ Math.round(speed) }} km per hour has a kinetic energy of about {{ (6800).toLocaleString(this.$i18n.locale) }} joules. If it hit someone at that speed, the shock would be similar that of a human body falling from twelve meters on concrete - a 100% chance of severe injury.<note content="A <a href='https://ntrs.nasa.gov/archive/nasa/casi.ntrs.nasa.gov/19930020462.pdf' target='_blank'>NASA paper from 1992</a> summarized experiments done in the field of survival to acceleration (see figure 9 page 35). A deceleration of 15m/s to 0 in .4 seconds is about 40 Gs, which NASA puts in the <em>area of severe injury</em>." note_number=1 />
                </p>
                <p>
                  This computation only gives orders of magnitude. Semi-trailers and SUVs are especially dangerous because of their ability to crush bodies under their wheels, for instance.<note content="For a description of how SUV kill more than sedans, see <a href='http://archive.is/nfiFx#selection-55.1-55.61' target='_blank'>Death on foot: America's love of SUVs is killing pedestrians</a>, a 2018 report by the Detroit Free Press." note_number=2 /> When two pedestrians or bicycles hit one another, each bears a share of the impact, making the shock for each one less intense. Each impact is unique but their outcome is always an issue of mass and speed.
                <p>
                  In an area where people can unexpectedly encounter your path, such as a city, if something bad happen while moving over a ton of steel at speeds over 12 km per hour, it cannot be called an accident. While some drivers are very careful to avoid impacts, moving around with enough energy to kill a person on the spot implies, <em>in itself</em>, some disregard for other people's lives. Bicycles, on the other hand, only become dangerous when driven over 40 km/h.
                </p>
                <p>
                  The disregard of car manufacturers and drivers for the life of others becomes blatant when looking at the evolution of safety devices. Pedestrian (external) airbags were first put into production in 2012 on the Volvo V40. As of 2018, no other Volvo model offers them.<note content='Some <a href="http://archive.is/Cot1L" target="_blank">background</a> on the Volvo pedestrian airbag. The same is true of the <em>Pedestrian Protection System</em> of Range Rover. It was introduced in 2014 on the Discovery Sport but has not been mounted on other models since then.' note_number=3 /> By contrast, passenger airbags were first introduced in the late 1980s and had become standard equipment in most cars in the early 1990s, less than five years later.<note content='On the history of passenger airbags, read the <a href="http://archive.is/bhhJJ#selection-439.0-439.18" target="_blank">History of Airbags</a> at Did You Know Cars.' note_number=4 /> Although the post-impact survival of pedestrians (since 2009) and cyclists (since 2018) has become part of the safety ratings made by Euro NCAP, a para-governmental organization that makes safety ratings for cars, the industry has yet to make it a standard and market it accordingly - and regulators have yet to make external airbags mandatory.
                </p>
                <p>
                  Driving a car over 12 km/h in a city is like using a flame-thrower instead of a lighter to start a fire. It can be done but it shows some disrespect to those stitting around the fire pit.
                </p>
                <p>
                  Of course, moving at 12 km/h would bring trouble to any a car driver, not least from the police. Urban planning in the last 70 years made it close to impossible for anyone unable to afford city-center accomodation to live normally without a car. Cars are a problem that goes far beyond individual decisions.
                </p>
                
                <h3>But cars are useful, aren't they?</h3>
                
                <p>
                  Conventional argumentation might recognize the greater danger cars pose and balance it against the benefits they provide. The evidence, however, does not support this view.
                </p>
                <p>
                  One reading of the history of private cars sees them as a replacement for horse carriages, which were everywhere in city streets at the beginning of the 20<sup>th</sup> century. Drowning in horse manure and deafened by the clicketing of horseshoes on cobblestones, city authorities welcomed and adopted the automobile as a faster, healthier solution. But, at least as early as the 1950s, astute observers were regretting that cities were so clogged in traffic that horse buggies would probably be faster.<note content="Salisbury, Harrison. <em>Study Finds Cars Choking Cities As 'Urban Sprawl' Takes Over</em>, New York Times, 3 March 1959. Quoted in Jane Jacob's <em>The Death and Life of Great American Cities</em>." note_number=5 /> And at least as early as the 1970s was the evidence becoming clear that car driving was unhealthy not only for people crushed by or breathing the exhaust of cars, but also for drivers themselves, who suffered from high blood pressure and low life satisfaction.<note content='An early study on the effects of car commute on health (there are many, many more): Stokols, Daniel, et al. "Traffic congestion, Type A behavior, and stress." <em>Journal of Applied Psychology</em> 63.4 (1978): 467.' note_number=6 />
                <p>
                  If cars were means of transportation comparable with mass transit and bicycle, they should have evolved to maximize their usefulness (moving people around) and minimize their drawbacks for buyers (reduced car size for easier parking, lower energy consumption and lower acquisition and maintenance costs). While the Smart Fortwo and Renault Twizy did go in this direction, they are far from being market leaders. Instead, larger, more cumbersome cars are advertised as adequate for in-city use and prove more popular with buyers. The 4-meter-long Audi Q2, for instance, branded as a city-SUV, sold more units in its first two years in Germany alone than the Renault Twizy globally since it was introduced in 2012.<note content='The <a href="http://archive.is/0Q9RL" target="_blank">Q2 official web page</a> makes no pretence that the car should be driven outside of a city. Sales figures come <a href="http://archive.is/ckqZo" target="_blank">from</a> the German Automobile Authority and <a href="http://archive.is/OtHw4" target="_blank">from</a> Renault.' note_number=7 />
                <p>
                  Average traffic speed in Paris is 16km/h, it is 25km/h in London (both measures include highways, street-level speed is lower).<note content='The figures for <a href="http://archive.is/z6C8a" target="_blank">Paris</a> and <a href="http://archive.is/r1xx8" target="_blank">London</a> come from local studies carried out by transport authorities and quoted in the press.' note_number=8 /> Taking into account the time needed to find a parking spot, inner-city travel by bicyle or mass transit is very often faster. Time efficiency is not a good reason to drive. Health cannot be either, for driving is detrimental to the driver's health while cycling improves it.<note content='On the health effects of cycling and driving, this cost-benefit analysis of driving and cycling contains a good overview of the literature: Gössling, Stefan, and Andy S. Choi. "Transport transitions in Copenhagen: Comparing the cost of cars and bicycles." <em>Ecological Economics 113</em> (2015): 106-113.' note_number=9 /> Another oft-quoted reason to prefer driving is comfort. But there are many ways to achieving comfort, such as sex or masturbation, which do not require the time, financial and health burden of driving.
                <p>
                  Of course, cars are status symbols. But why do people not buy gold-plated Twizys to show their social standing? Why do they, instead, buy objects that harm them and that perform their stated mission (move people) terribly badly? The only logical answer is that cars are not made to transport people but to show status. Exhaust emissions, noise and, above all, the ability to kill are not regrettable byproducts of a means of transportation. They are the intrinsic qualities of a good that is primarily meant to display superiority. That cars can move people around is the byproduct.
                </p>
                <p>
                  Don't get me wrong, I love driving. I just believe that it should be seen for what it is: a recreational activity for people who love expensive, polluting toys. Cars belong in the same category as Jet Skis or quads.
                </p>
                
                <h3>Cars and cigarettes</h3>

                <p>
                  Cars are woefully inadapted to transport people within cities.<note content="On the unability of cars to transport people, see Arieff, Allison. <a href='https://www.nytimes.com/interactive/2018/02/27/opinion/automated-vehicles-cant-save-cities.html' target='_blank'>Automated Vehicles Can't Save Cities</a>, New York Times, 27 February 2018." note_number=10 /> Despite this shortcoming, car driving is heavily subsidized and encouraged by all governments and administrations, bar the handlful of towns that reorganized themselves to get rid of private vehicles.<note content="Ponteverda in Spain, for instance. (<a href='https://www.theguardian.com/cities/2018/sep/18/paradise-life-spanish-city-banned-cars-pontevedra' target='_blank'>See this Guardian article</a>.) Wikipedia has an interesting <a href='https://en.wikipedia.org/wiki/List_of_car-free_places' target='_blank'>list of car-free places</a>." /> That goverments push destructive policies is nothing new. Car driving should be put in the same category as other government programs with extremely negative outcomes, such as smoking.<note content="On the history of government responses to smoking, I use mostly Robert Proctor's <em>Golden Holocaust</em>." />
                </p>
                <p>
                    Arguing that cars are a means of transportation is a bit like arguing that cigarettes are for helping digestion. It sounds absurd now, but it was a common theme in cigarette advertising in the 1930's.<note content="<a href='https://www.thecrimson.com/article/1936/2/28/for-digestions-sake-smoke-camels-plife-gets/' target='_blank'>For digestion's sake, smoke Camels</a> was a common advertising theme until the 1930's." note_number=11 /> Cars and cigarettes share much more than misleading advertising. Both are status symbols, used first by white men and second by those who sought to emulate them. Enticing self-assertive women to buy SUVs is not different from pushing them towards smoking two generations ago.
                </p>
                <p>
                  Cars, unlike cigarettes, are not addictive. While any effort to curb smoking only becomes visible when a new cohort of non-smokers comes of age (current smokers are unlikely to cure their addiction before they die),<note content="A longitudinal study in the United Kingdom showed that one in five smokers quit over a period of 10 years. I could not find data on lifelong quitters but I suspect the number is lower. Chandola, T., Head, J., & Bartley, M. (2004). Socio-demographic predictors of quitting smoking: how important are household factors? Addiction, 99(6), 770–777." note_number="12" /> curbs on car driving will have immediate effects.
                </p>
                <p>
                  However, the history of the fight against smoking teaches a sobering lesson. Rationality never had a chance against the power of tobacco companies and the spinelessness of government officials. The arguments against smoking were rock-solid by 1964, when the United States' highest health authority published a report on the harms of smoking (other government branches subsequently did nothing to stop the smoking epidemic).
                </p>
                <p>
                  It was only in the 1990s that cigarette manufacturers began to lose the fight in the U.S. and, a few years later, in Europe. The direct reason is that judges began to rule in favor of plaintiffs (usually smokers with cancer),<note content='Douglas, Clifford E., Ronald M. Davis, and John K. Beasley. "Epidemiology of the third wave of tobacco litigation in the United States, 1994–2005." Tobacco control 15.suppl 4 (2006): iv9-iv16.' /> culminating in the Master Settlement Agreement of 1998 when top tobacco companies agreed to pay for some of the health care bills of smokers. While I could not find research on why the reversal happened in the early 1990s, I suspect that the cigarette industry decided to abandon the fight in the U.S. to invest more in China and the former Soviet Union, two much larger markets that opened at the time.
                </p>
                <p>
                  Private cars are closer to cigarettes than to any means of transportation. The history of the fight against tabacco shows that victory of health and life over cars will require much more than sound arguments.
                </p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>

  import navbar from './Navbar.vue'
  import shareitem from './shareItem.vue'
  import calculator from './Calculator.vue'
  import note from './Note.vue'

  export default {
    name: 'Home',
    components: {
      navbar,
      shareitem,
      note,
      calculator
    },
    data () {
      return {
        weight: 65,
        speed: 12,
        vehicle: {'type': 'car', 'weight': 1200}
      }
    },
    methods: {
      updateVars(computedVars) {
        this.weight = computedVars.weight
        this.vehicle = computedVars.vehicle
        this.speed = computedVars.speed
      }
    },
    computed: {
      total_weight() {
        var total_weight = this.weight + this.vehicle.weight
        if (this.vehicle.type == "pedestrian") { return Math.round(total_weight) + " kg" }
        else if (total_weight < 1000) { return Math.round(total_weight) + " kg"}
        else { return (total_weight / 1000).toFixed(1) + " tons"}
      }
    }
  }
</script>

<style lang="sass">
@import "colors.sass"
$family-primary: "Arial"
$title-size: 2.5em
$weight-semibold: 200
$body-family: "Arial"
$primary: $nkb-purple
$info: $nkb-lightblue
$link: $nkb-darkblue
$success: $nkb-yellow
$danger: $nkb-red

@import "~bulma/bulma"

h1
  font-weight: 200

.article-content
  font-size: 1.2rem
  line-height: 2rem
  font-family: Georgia

.byline
  font-variant: small-caps
  font-size: .8rem
  font-family: Georgia
</style>
