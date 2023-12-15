---
geometry: "left=1in,right=1in,top=1in,bottom=1in"
fontfamily: times
fontsize: 12pt
output: pdf_document
header-includes:
        - \usepackage{times}
        - \usepackage{tcolorbox}
        - \renewtcolorbox{quote}{}
---

# RSTB-2023-0166 Author response to reviewers

We would like to thank both reviewers for their helpful input on our manuscript. Following their comments, we did two main changes to our manuscript. First, we added an analysis of network motifs across ecoregions to further explore the variation in network structure across space, as both reviewers suggested. We added a new figure with those results (now Fig. 4). We decided to move our previous Fig. 3 (showing the bivariate relationships between community and network measures) to Supplementary Material (now Fig. S1) to respect the Journal's limit on the number of figures. However, we will gladly put it back in the main text if the Editor judges that we have room for it.

Second, we followed Reviewer 1's suggestion regarding pseudo-absences and changed our random selection algorithm for one which weights candidate sites by their distance to an observation, making it more likely to select sites further away from observed ones. We believe that doing so allows us to better represent the potential distributions of species, as Reviewer 1 mentioned. Consequently, we re-ran our species distribution models and updated our figures given the new distributions. This does not change the conclusions from our manuscript, except for one result which is worth discussing below. Otherwise, our results are very consistent, notably regarding the latitudinal gradients of species richness and number of links, the differences in the spatial distributions of ecoregion median values and within-ecoregion variance, and the contrast between hotspots of network and species uniqueness.

The one result which differs from our previous version is the mismatch in the distributions of species richness and number of links that we reported in our earlier analyses. As we can see on our updated Fig. 1 and Fig. S1, both spatial distributions now follow each other quite closely, while they showed clear differences before. Nonetheless, we believe this result follows logically from the change of focus towards potential distributions and is preferable for two reasons. First, as Reviewer 1 pointed out, modelling potential distributions and wider responses to the environment makes more sense to go along with the metaweb concept. The metaweb and its downscaled localized version we present here are highly potential in nature and aim to serve as an upper boundary for what the interactions could be at a local scale. Therefore, using potential distributions ensures that we capture the widest potential output given the environment. Second, changing the pseudo-absence generation method smoothed out the results for species richness and reduced over-fitting towards the cities, which we think is more appropriate here (see the previous and updated richness figures below). As we now select pseudo-absences further away from the species occurrences, our distribution models essentially do in-filling within the observed species range and is likely to generate distributions with less holes. Notably, species richness increased in most areas, now reaching a maximum around 100 compared to 85 before (as visible on the figure below). Consequently, the number of links increased even more than richness (from a maximum around 700 links up to 850 links). Given the increase in richness, species can realize their interactions with the highest probabilities in more locations except in very poor sites. Doing so, we believe it normal to observe an better agreement between the two distributions, as there is now less of a spatial constraint on where species can realize their interactions.

Please also find below is our point-by-point response to comments from the reviewers.

\renewcommand{\thefigure}{R\arabic{figure}}

![Previous site-level richness map](figures/richness_mean_previous.png){#fig:previous height=45%}

![Updated site-level richness map](figures/richness_mean.png){#fig:updated height=45%}

## Reviewer 1

> Thank you for a great paper. I really like the design of your workflow, and I think it provides a sound and solid way of downscaling the metawebs into ecoregion or local webs, that could foster new analyses of different taxa and regions. Just to be clear, I believe the structure of your workflow seems quite sound to me, and the way it embeds probabilistic measures of potential distributions and potential interactions may help modelling the variability that local networks may have in nature in a realistic way. In fact, I do look forward to see comparisons of these potential networks with empirical networks (and where do realized networks lie within the possible networks), but that’s a different step, that first requires developing the analytical framework that you are presenting here. I only have two major suggestions which, I believe, would sharpen and strengthen your workflow, and a specific comment.  

We are grateful to Reviewer 1 for their kind words and understanding of our manuscript.

> Why do you use random pseudoabsences within the species range to construct the Species Distribution Models if you want to represent the potential distribution? You do it throughout all the range of the data, but that includes both areas within the species range, and areas outside of it. I’m telling this because the decision is not meaningless in terms of whether you model current distributions (where including absences in places within the range to include areas that could host presences but are unoccupied by the species matters) or potential distributions (where capturing the wider responses to the environment is what matters). That is, capturing where the species is vs where the species could be. A consequence of this is that how you pick pseudoabsences is a key choice, and I believe you may have taken the wrong direction. There are examples in the literature about how to make this choice, but if you would create them from outside of the observed range of the species, or assigning lower probability to choosing non-sampled places within the known species range I believe your models will represent potential distribution much better. If you do so, this should be much clear in the text.  

- We understand the reviewer's concerns and agree with them
- Our intent is to model the potential distribution
- Consequently we changed the pseudoabsence generation method for the DistanceToEvent one, which weight candidate sites by their distance to an observation, making it more likely to select sites further away from observed ones
- Add justification from Barbet-Massin et al.?
- See [[2023-12-13#Catch-up]]
  
> Your spatial comparison between richness and network size is so great that I wonder whether you do not explore other aspects of network structure, such as nestedness and modularity. These metrics may help understanding better the spatial mismatches between richness and number of links shown in figs 3 and 4, as if I’m getting it correctly, these may be caused by the selection of a handful modules in the northern ecoregions, compared to more connected networks towards the south-southwest.  

- We added an analysis of motifs
- We chose motifs over nestedness and modularity as they are ecologically meaningful and have a clear interpretation
- ==Brush over mismatch betweeb richness and links?==

> Line 162; rather than potential effects (which to me includes all potential variation associated to the probabilistic models) I would say “main/overall trends promoted by environmental gradients”, or something similar, emphasizing that the variability creates “noise” in local networks, but that such “noise” is realistic.  

- We added this suggestion
  
> Besides these three things, my only concern is that the results could perhaps allow to explore further the gradients in network structure (related also with my second major comment), which me being a biogeographer is perhaps unsurprising. I however would like to see you further explorations of this facet of your results; if not here, in other papers.  

- See description of motifs

\newpage
## Reviewer 2

### General comment
> Dansereau et al. use a predicted tetrapod metaweb to predict the structure of mammal food webs for Canada at the local scale. I enjoyed reading the paper and applaud the authors for their efforts in predicting species interactions in space, which is a monumental task, and hard, maybe even impossible, to achieve empirically. All in all, the work by Dansereau et al. 2023 is very impressive and deals with a topic of high relevance and importance for food web ecology, and beyond. Especially, the enormous pipeline of computations behind this work is truly impressive and inspiring. The framework presented opens many new opportunities and holds great potential for improving predictive food web ecology. It especially nice to see that this approach allows for capturing variability in trophic interactions at the local food webs. 

We are thankful to Reviewer 2 for their acknowledgement of the work we put into this manuscript.

> That said, I do have some concerns and questions regarding the realism and validity of the predictions, based on species distribution data outside of the target region (Canada), and on a predicted metaweb based on species interactions from a different continent, which results in predictive algorithms trained on data outside the target region(s). Moreover, the study bases prediction upon prediction in a long pipeline of predictions, are there any risk involved with this in terms of how realistic the networks are? Could you add some reflections about this in the main text.  

- Point out that the Canadian metaweb was validated
- SDMs are also validated
- We intend to represent potential networks and distributions
- We want to show the potential variation in space

> In the following, I would like to ask some clarifying questions about the premise of this work and the choices made, which I also think should be made clearer in the main text. As far as I understand it, the accuracy of the metaweb is important for the accuracy of the local food web predictions, which in turn is important for the local webs to be actionable, one of the ultimate goals with this work.  

- Repondre un petit truc. Clarifier ce qui est important ou non

> Without comparing the predicted output to observed data, how sure can you be that the predicted food webs reflect actual food web realizations? Therefore, a validation of the results should be added to the paper, and this should also be discussed. There must be some field sampled information on mammals in Canada for some of the defined ecoregions which you could use for comparing the predicted species composition of the food webs to observed ones. For the predictions to be actionable, this would seem an important step.  

- As Reviewer 1 pointed out we present an analytical framework first and foremost
- Summary results, such as motifs, will be easier to validate than entire networks, especially at the ecoregion level
- Validation would be relevant, but data availability is an issue
- Issues with available data
	- Newfoundland: not spatial, already used for Canadian metaweb
	- Arctic food webs: few species
	- Marine motifs: marine species
	- Problème déjà existant pour validation metaweb, trop circulaire de revalider. Peut pas faire sans pseudo replication
- Recommender comment on devrait valider par la suite

> If I understand correctly, for the predictions behind this study to work, field sampled observations are necessary - that is the European tetrapod metaweb based on field observations were essential to make the predicted Canadian metaweb. I find this fundamental premise of the metaweb construction underreported in this paper. Despite all the help computers can provide in making highly resolved predictions of species interactions in space, they still need high quality input data based on field observations to work properly. This point is not trivial, especially not for the “actionability” of the predictions. This should be acknowledged in the paper.  

- The European tetrapod metaweb is based on expert knowledge and litterature review, not field observations, although this also requires tremendous work
- Yes, our framework does require a metaweb, but it could be applied to any one. We use the probabilistic value here, but it doesn't have to be. (as we discuss in the Discussion)
	- Surtout si incertitude à échelle des interactions
	- Couper en 2. Oui étape suivante est validation empirique. 
	- Si on avait pas ce problème, pas d'infos sur où regarder pour réseaux.
	- Carte dit où regarder et à quel endroit, pas les réseaux complets. Mais on s'attend à gradients biogéo raisonnables
	- Qu'est-ce qu'on suggère comme utilisation des résultats et ce qui n'est pas faisable
	- On apprécie les inquiétudes
- Lack of input data is one the point of Tanya's manuscript: when we don't know, we can infer from somewhere else
	- But this is not the point of our paper
- Also from Tanya's perspective manuscript: a metaweb is sometimes "simpler" to obtain than localized network values in multiple locations

> Generally, I find the description of the metaweb and the assumptions behind it too sparse. How big is the metaweb? How many species, links and trophic levels does it contain? Does it only contain mammals? What resource species (prey) does it contain? Is it just mammals preying on other mammals? Could you provide a network of the metaweb in the SI with some more information?  

- We added more information on the metaweb relevant to this paper
- But we are not creating the metaweb here, we're reusing it from another manuscript

> This leads me to another important question, why were only species richness and number of link density calculated as network properties. Strictly, speaking you would not have needed a food web approach to calculate these two properties. It would have been more interesting if you would have provided analyses of connectance, and in- and out-degree, in space? How was the choice of metrics made, could you please add a justification to the paper.  

- We added a motifs analysis which makes use of the food web approach
- Connectance is in supp.mat. The spatial distribution exactly matches the number of links as, following Poisot et al. 2016's probabilistic definitions, it is the number of link divided by the number of species in the metaweb (159)
- Previous studies such as Gravel et al. 2019, Braga et al. 2019 use number of links/connectance as their main network property in space

> Finally, while the paper is generally well-written, the clarity of some parts of the text could still be improved.  

### Detailed comments

We incorporated most of the suggestions from Reviewer 2 in the updated manuscript. All changes are listed in the additional Track Changes file. Here, we further provide responses to a few specific comments from the Reviewer.

> Data:  
> L. 111. Why did you include species distributions and occurrences (long. and lat.) outside of Canada, and as far south as central America? Does it improve your predictions? Did you make a test run with species ranges restricted to Canada, or North America? What happens to your predictions/results if you are more conservative in your species range? I wonder whether including data from so far south can result in an over- or under- representation of certain species in some of your ecoregions, especially in the southern parts of Canada, could it? Could you provide a test with a more conservative species range more closely reflecting the biogeography of Canada, or at minimum justify your choice and its implications.  

- Training SDMs on a wider range is a standard practice
- Species were selected for the Canadian Metaweb according to IUCN
- We want to include species even if only the southern part of their range is in Canada

> L. 114. Can the random choice of pseudo-absences in space influence the outcome, or does this computational step not have any effect on the results at all?  

- The method to select pseudo-absences does have an effect, as shown with our updated result
- We believe the DistanceToEvent method will be more appropriate to model the potential distribution of the species, as suggested by Reviewer 1
  
> L. 213. What are the localized interaction values? What do you mean by “interaction value”, the interaction probability, mean/median no. of links at a given site? This is not clear. 
  
> L. 242. Are the expected median values per ecoregions based on a median binary summary web of the many versions of the localized metawebs, or did you calculate species richness and number of links per species for the many versions of the localized metawebs and then take the median? Could you make this clearer. How are the probabilities of the interactions reflected in these median values? … because rare interactions are less often predicted and hence the median number of links per species would be lower?  

- The median values represent the median across all sites in the ecoregion
- Species richness and number of links are first calculated on the localized metawebs
- Then we calculate the median value across all sites in the ecoregion and attribute this value for the ecoregion
- An ecoregion with a high median for the number of links could either have interactions with a very high probability or many interactions with a lower probability

> Discussion:  
> L. 301. Are you comparing your predicted mammal food web from Canada to the observed tetrapod food web in Europe, the latter which includes more species, especially at lower trophic levels (I assume)? Is this meaningful at all?  

- We recognize this is not the best comparison (as we mention in the text)
- However, we think it's relevant to mention here as it is the closest comparison of a metaweb structure in space

> L. 302. It would have been nice if you could reflect upon and elaborate in which way the data and methodology could have influenced the results. The same for biogeography.  
 
> L. 303. There should be differences between Europe and Canada due to varying climatic conditions at the same latitudes. Due to the Gulf stream northern areas of Europe are much milder in e.g., temperature than regions in Canada, so it makes sense that the food webs differ in connection given that temperatures influence species trophic interactions and food web properties.  

- We emphasized that we show examples of the potential distribution of the network metrics, not a detailed analysis of network structure in Canada.

> Figures:  
> The figures are pretty, but it was impossible to read the color code (blue-green shading) on a grey color scale print out.  

- We chose this specific color palette as there are very few colorblind-friendly ones

> Fig. 3b. Could the higher variation in the predictions in the southernmost part of Canada be because the predictions were trained on data of species occurrences (distributions) outside the range of Canada?``