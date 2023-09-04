# Introduction

Sampling species interactions and ecological networks in repeated locations in
space and time is a challenging task [@Jordano2016SamNet]. Most studies on food
webs have previously focused on local webs limited in size and extent, and are
rarely replicated in space and time [@Mestre2022DisFoo]. Available network data
also show important geographical bias, limiting our ability to answer questions
in many biomes and over broad spatial extents [@Poisot2021GloKno]. Yet, we know
that interactions can show important variations in space [@Poisot2015SpeWhy] and
that they are critical to evaluating how ecosystems will react to global change.
Even predictive approaches [@Desjardins-Proulx2017EcoInt;
@Morales-Castilla2015InfBio], seen as a way to circumvent data scarcity
[@Strydom2021RoaPre], often do not have an explicit spatial component. As a
result, there have been repeated calls for globally distributed interaction and
network data and repeated samplings in time and space [@Mestre2022DisFoo;
@Poisot2021GloKno]. 

A promising concept gaining momentum for the analysis of networks in space is
that of the metaweb. A metaweb contains all the possible interactions between
the species found in a given regional species pool [@Dunne2006NetStr]. Studies
are now directly focused on assembling metawebs for various taxa through
extensive literature surveys [@Maiorano2020TetSpe] or using predictive tools
[@Strydom2022FooWeb]. These new data sources have allowed studying network
structures in novel ways, for instance, assessing changes in food web structure
across space [@Braga2019SpaAna], the scaling of network area relationships
[@Galiana2021SpaSca], or how sampling effort affects measured network structure
[@McLeod2021SamAsy]. A key element that emerged from these studies is that the
structure of empirical food webs is inherited from the metaweb with little
influence from habitat and dynamical constraints [@Saravia2022EcoNet]. This
makes the metaweb the core goal of predictive network ecology
[@Strydom2022PreMet], i.e. the first approximation of networks in space we
should aim for. Yet, rather than directly predicting the metaweb and localized
networks, some studies have instead focused on using interactions to improve
predictions of species distributions [for example, @Poggiato2022IntFoo;
@Lucas2023IncBio; @Moens2022ImpBio], answering long-standing calls to include
interactions within such models [@Wisz2013RolBio]. However, refining predictions
of species distributions through interactions differs from predicting networks
in space; it serves a different goal and does not fully consider networks as
spatial elements.

Two network aspects are essential to develop a proper spatial perspective.
First, networks are local realizations of a regional metaweb [@Poisot2012DisSpe;
@Poisot2015SpeWhy], which reinforces why the metaweb should be predicted first.
Second, to account for their variability in space, interactions must be seen as
probabilistic events [@Poisot2016StrPro]. In contrast, many studies assume
interactions are binary events, whether at the interaction, network or metaweb
level [@Gauzere2022DivBio; @Mendoza2022BioBir]. However, a probabilistic view
can additionally allow propagating uncertainty, which can play a key role in
evaluating the quality of the predictions. Moreover, assessing model uncertainty
would enable us to assess to which degree we should trust our predictions and to
identify what to do to improve the current knowledge. For instance, we could
locate where our knowledge and models are the most uncertain and determine new
sampling sites or areas where repeated sampling is necessary.

Repeated network samples and explicit spatial predictions are essential as they
will allow comparisons with extant work for species communities. These
comparisons are relevant as they may go in unexpected directions and highlight
new elements regarding network biogeography. For instance, @Frelat2022FooWeb
found a strong spatial coupling between community composition and food web
structure but a temporal mismatch depending on the spatial scale.
@Poisot2017HosPar found that interaction uniqueness captures more composition
variability than community uniqueness and that sites with exceptional
compositions might not be the same for networks and communities. Spatialized
network data will allow these comparisons and allow identifying important
conservation targets for networks from areas currently prioritized for
biodiversity conservation.

Here, we present a method to downscale a metaweb in space by spatially
reconstructing local instances of a probabilistic metaweb of Canadian mammals.
We explore how the spatial structure of the downscaled metaweb varies in space
and how the uncertainty of interactions can be made spatially explicit. We
further show that the downscaled metaweb can highlight important biodiversity
areas and bring novel ecological insights compared to traditional community
measures like species richness.

# Methods

@Fig:conceptual shows a conceptual overview of the methodological steps leading
to the downscaled metaweb. The components were grouped as non-spatial and
spatial inputs, localized steps (divided into single-species-level,
two-species-level, and network-level steps), and the final downscaled and
spatialized metaweb. Throughout these steps, we highlight the importance of
presenting the uncertainty of interactions and of their distribution in space.
We argue that this requires adopting a probabilistic view and incorporating
variation between scales.

![Conceptual figure of the workflow to obtain the spatial probabilistic metaweb
(Chapter 1). The workflow has three components: the inputs, the localized steps,
and the final spatial output. The inputs are composed of the spatial data (data
with information in every cell) and the non-spatial data (constant for all of
Canada). The localized steps use these data and are performed separately in
every cell, first at a single-species level (using distribution data), then for
every species pair (adding interaction data from the metaweb), and finally at
the network level by combining the results of all species pairs. The final
output coming out of the network-level steps contains a spatialized
probabilistic metaweb for every cell across the study
extent.](figures/conceptual-figure.png){#fig:conceptual}

## Non-spatial inputs

The main source of interaction data was the metaweb for Canadian mammals from
@Strydom2022FooWeb, which is a-spatial, i.e., it represents interactions between
mammals that can occur anywhere in Canada. The species list for the Canadian
metaweb was extracted from the International Union for the Conservation of
Nature (IUCN) checklist [@Strydom2022FooWeb]. Briefly, the metaweb was developed
using graph embedding and phylogenetic transfer learning based on the metaweb of
European mammals, which is itself based on a comprehensive survey of
interactions reported in the scientific literature [@Maiorano2020TetSpe]. The
Canadian metaweb is probabilistic, which has the advantage of taking into
account that species do not necessarily interact whenever they co-occur
[@Blanchet2020CoOcc]. However, since the Canadian metaweb is not explicitly
spatial, it only gives information on interactions in Canada as a whole and does
not represent networks at specific sites. Local networks, on the other hand, are
realizations from the metaweb resulting from sorting the species and the
interactions [@Poisot2015SpeWhy]. A spatial and localized metaweb is not
equivalent to the local networks, as it will have a different structure and a
higher connectance [@Strydom2022PreMet]. Therefore, producing a spatial metaweb
requires additional steps to account for species composition and interaction
variability in space.

### Spatial inputs

The downscaling of the metaweb involved combining it with species occurrence and
environmental data. First, we extracted species occurrences from the Global
Biodiversity Information Facility (GBIF; www.gbif.org) for the Canadian mammals
after reconciling species names between the Canadian metaweb and GBIF using the
GBIF Backbone Taxonomy [@GBIFSecretariat2021GbiBac]. Doing so, we removed
potential duplicates where species listed in the Canadian metaweb are considered
as a single entity by GBIF. We collected occurrences for our species list (159
species) using the GBIF download API on October 21st 2022 [@GBIF.org2022GbiOcc].
We restricted our query to occurrences with coordinates between longitudes 175°W
to 45°W and latitudes 10°N to 90°N. This was meant to collect training data
covering a broader range than our prediction target (Canada only) and include
observations in similar environments. Then, since GBIF observations represent
presence-only data and most predictive models require absence data, we generated
pseudo-absence data using the surface range envelope method available in
`SimpleSDMLayers.jl` [@Dansereau2021SimJl]. This method generates
pseudo-absences by selecting random non-observed sites within the spatial range
delimited by the presence data [@Barbet-Massin2012SelPse]. 

We used species distribution models [SDMs, @Guisan2005PreSpe] to project
Canadian mammal habitat suitability across the country, which we treated as
information on potential distribution. For each species, we related occurrences
and pseudo-absences with 19 bioclimatic variables from CHELSA
[@Karger2017CliHig] and 12 consensus land-cover variables from EarthEnv
[@Tuanmu2014Glo1km]. The CHELSA bioclimatic variables (_bio1-bio19_) represent
various measures of temperature and precipitation (e.g., annual averages,
monthly maximum or minimum, seasonality) and are available for land areas across
the globe. We used the most recent version, the CHELSA v2.1 dataset
[@Karger2021CliHig], and subsetted it to land surfaces only using the CHELSA
v1.2 [@Karger2018DatCli], which does not cover open water. The EarthEnv
land-cover variables represent classes such as Evergreen broadleaf trees,
Cultivated and managed vegetation, Urban/Built-up, and Open Water. Values range
between 0 and 100 and represent the consensus prevalence of each class in
percentage within a pixel (hereafter considered as sites). We coarsened both the
CHELSA and EarthEnv data from their original 30 arc-second resolution to a 2.5
arc-mininute one (around 4.5 km at the Equator) using GDAL
[@GDAL/OGRcontributors2021GdaOgr]. This resolution compromised capturing both
local variations and broad scale patterns, while limiting computation costs to a
manageable level as memory requirements increase rapidly with spatial
resolution.

Our selection criteria for choosing an SDM algorithm was to have a method that
generated probabilistic results, including both a probability of occurrence for
a species in a specific site and the uncertainty associated with the prediction.
These were crucial to obtaining a probabilistic version of the metaweb as they
were used to create spatial variations in the localized interaction
probabilities (see next section). One suitable method for this is Gradient
Boosted Trees with a Gaussian maximum likelihood from the `EvoTrees.jl` *Julia*
package (https://github.com/Evovest/EvoTrees.jl). This method returns a
prediction for every site with an average value and a standard deviation, which
we used as a measure of uncertainty to build a Normal distribution for the
probability of occurrence of a given species at all sites (represented as
probability distributions on @Fig:conceptual). We trained models across the
extent chosen for occurrences (longitudes 175°W to 45°W and latitudes 10°N to
90°N), then predicted species distributions only for Canada. We used the 2021
Census Boundary Files from Statistics Canada [@StatisticsCanada2022BouFil] to
set the boundaries for our predictions, which gave us 970,698 sites in total.

## Localized steps: Building site-level instances of the metaweb

The next part of the method was the localized steps which produce local metawebs
for every site. This component was divided into single-species, two-species, and
network-level steps (*Localized steps* box on @Fig:conceptual).

The single-species steps represented four possible ways to account for
uncertainty in the species distributions and bring variation to the spatial
metaweb. We explored four different options to select a value (_P(occurrence)_;
[@Fig:conceptual]) from the occurrence distributions obtained in the previous
steps (Inputs section): 1) taking the mean from the distribution as the
probability of occurrence (option 1 on @Fig:conceptual); 2) converting the mean
value to a binary one using a specific threshold per species (option 2); 3)
sampling a random value within the Normal distribution (option 3); or 4)
converting a random value into a binary result (option 4, using a separate draw
from option 3 and the same threshold as in option 2). The threshold ($\tau$ on
@Fig:conceptual) used was the value that maximized Youden's *J* informedness
statistic [@Youden1950IndRat], the same metric used by @Strydom2022FooWeb at an
intermediate step while building the metaweb. The four sampling options were
intended to explore how uncertainty and variation in the species distributions
can affect the metaweb result and doing so reproduce some of the filterings that
create the local network realizations [@Poisot2015SpeWhy]. We expected
thresholding to have a more pronounced effect on network structure as it should
reduce the number of links by removing many of the rare interactions
[@Poisot2016StrPro]. Meanwhile, we expected random sampling to create spatial
heterogeneity compared to the mean probabilities, as including some extreme
values should confound the potential effects of environmental gradients.

Next, the two-species steps were aimed at assigning a probability of observing
an interaction between two species in a given site. For each species pair, we
multiplied the product of the two species' occurrence probabilities
(_P(co-occurrence_; Fig. 1) (obtained using the one of the sampling options
above) by their interaction probability in the Canadian metaweb. For cases where
species in the Canadian metaweb were considered as the same species by the GBIF
Backbone Taxonomy (the reconciliation step mentioned earlier), we used the
highest interaction probabilities involving the duplicated species.

The network-level steps then created the probabilistic metaweb for the site. We
assembled all the local interaction probabilities (from the two-species steps)
into a probabilistic network [@Poisot2016StrPro]. We then sampled several random
network realizations to represent the potential local realization process
[@Poisot2015SpeWhy]. This resulted in a distribution of localized networks,
which we averaged over the number of simulations to obtain a single
probabilistic network for the site.

## Outputs: The downscaled metaweb

The final output of our method was the spatial probabilistic metaweb, which
contains a localized probabilistic metaweb in every cell across the study area
(Outputs box on @Fig:conceptual). This gives us an idea of the possible networks
in all sites as the metaweb essentially serves to set an upper bound on the
potential interactions [@Strydom2022PreMet], but with the added benefit of
accounting for co-occurrence probabilities in this case. From there, we can
create maps of network properties (e.g. number of links, connectance) measured
on the local realizations, display their spatial distribution, and compute some
traditional community-level measures such as species richness. We can also
calculate the uncertainty associated with the network and community measurements
and compare their spatial distribution (see Supplementary Material). 

### Analyses of results by ecoregions

Since both species composition and network summary values display a high spatial
variation and complex patterns, we simplified the representation of their
distribution by grouping sites by ecoregion, as species and interaction
composition have been shown to differ between ecoregions across large spatial
scales [@Martins2022GloReg]. "To do so, we rasterized the Canadian subset of the
global map of ecoregions from @Dinerstein2017EcoApp [also used by
@Martins2022GloReg], which resulted in 44 different ecoregions. For every
measure we report (e.g. species richness, number of links), we calculated the
median site value for each ecoregion. We also measured within-ecoregion
variation as the 89% interquantile range of the site values in each ecoregion
[threshold chosen to avoid confusion with conventional significance tests\;
@McElreath2020StaRet].

### Ecological uniqueness

We compared the compositional uniqueness of the networks and the communities to
assess whether they indicated areas of exceptional composition. We measured
uniqueness using the local contributions to beta diversity [LCBD,
@Legendre2013BetDiv], which identify sites with exceptional composition by
quantifying how much one site contributes to the total variance in the community
composition. While many studies used LCBD values to evaluate uniqueness on local
scales or few study sites [for example, @daSilva2014LocReg; @Heino2017ExpSpe],
recent studies used the measure on predicted species compositions over broad
spatial extents and a large number of sites [@Vasconcelos2018ExpImp;
@Dansereau2022EvaEco]. LCBD values can also be used to measure uniqueness for
networks by computing the values over the adjacency matrix, which has been shown
to capture more unique sites and uniqueness variability than through species
composition [@Poisot2017HosPar]. Here, we measured and compared the uniqueness
of our localized community and network predictions. For species composition, we
assembled a site-by-species community matrix with the probability of occurrence
at every site from the species distribution models. For network composition, we
assembled a site-by-interaction matrix with the localized interaction values
from the spatial probabilistic metaweb. We applied the Hellinger transformation
on both matrices and computed the LCBD values from the total variance in the
matrices [@Legendre2013BetDiv]. High LCBD values indicate a high contribution to
the overall variance and a unique species or interaction composition compared to
other sites. Since values themselves are very low given our high number of sites
[as in @Dansereau2022EvaEco], what matters primarily is the magnitude of the
difference between the sites. Given this, we divided values by the maximum value
in each matrix (species or network) and suggest that these should be viewed as
relative contributions compared to the highest observed contribution. As with
other measures, we then summarized the local uniqueness values by ecoregion by
taking the median LCBD value and measuring the 89% interquantile range within
all ecoregions.

We used _Julia_ v1.9.0 [@Bezanson2017JulFre] to implement all our analyses. We
used packages `GBIF.jl` [@Dansereau2021SimJl] to reconcile species names using
the GBIF Backbone Taxonomy, `SpeciesDistributionToolkit.jl` to handle raster
layers and species occurrences, `EcologicalNetworks.jl` [@Poisot2019EcoJl] to
analyse network and metaweb structure, and `Makie.jl` [@Danisch2021MakJl] to
produce figures. Our data sources (CHELSA, EarthEnv, Ecoregions) were all
unprojected and we did not use a projection in our analyses, but we displayed
the results using a Lambert conformal conic projection more appropriate for
Canada using `GeoMakie.jl`. All the code used to implement our analyses is
available on GitHub (https://github.com/PoisotLab/SpatialProbabilisticMetaweb)
and includes instructions on how to run a smaller example at a coarser
resolution. Note that running our analyses at full scale is resource and memory
intensive and required the use of compute clusters provided by Calcul Québec and
the Digital Research Alliance of Canada.

# Results

Our method allowed us to display the spatial distribution of ecoregion-level
community measures (e.g. expected species richness) and network measures (e.g.
expected number of links; [@Fig:ecoregion_measures]). We highlight that the
community and network-level measures presented here are not actual predictions
of the measure itself (e.g., we do not present a prediction of actual species
richness at each location). Instead, they are the reflection of these metrics
from the localized predictions of the communities and networks obtained from the
downscaling of the metaweb, then summarized for the ecoregions (median value).
Expected ecoregion richness ([@Fig:ecoregion_measures]A) and expected number of
links ([@Fig:ecoregion_measures]B) displayed similar distributions with a
latitudinal gradient and higher values in the south. However, within-ecoregion
variability was distributed differently, as some ecoregions along the coasts
displayed higher interquantile ranges while ecoregions around the southern
border displayed narrower ones ([@Fig:ecoregion_measures]C-D).  All results
shown are based on the first sampling strategy (option 1) mentioned in the
Localized steps section, where species occurrence probabilities were taken as
the mean value of the distribution (results for other sampling strategies are
discussed in Supplementary Material). 

![(A-B) Example of a community measure (A, expected species richness) and a
network one (B, expected number of links). Both measures are assembled from the
predicted probabilistic communities and networks, respectively. Values are first
measured separately for all sites, then the median value is taken to represent
the ecoregion-level value. (C-B) Representation of the 89% interquantile range
of values within the ecoregion for expected richness (C) and expected number of
links (D).](figures/ecoregion_comparison_iqr.png){#fig:ecoregion_measures}

Direct comparison of the spatial distributions of species richness and expected
number of links showed some areas with mismatches, both regarding the median
estimates and regarding the within-ecoregion variability
([@Fig:ecoregion_bivariates]). Median values for the ecoregions showed a similar
bivariate distribution with ecoregions in the south mostly displaying high
species richness and a high number of links ([@Fig:ecoregion_bivariates]A). The
northernmost ecoregions (Canadian High Artic Tundra and Davis Highlands Tundra)
displayed higher richness (based on the quantile rank) compared to the number or
links. Inversely, ecoregions further south (Canadian Low Artic Tundra, Northern
Canadian Shield Taiga, Southern Hudson Bay Taiga) ranked higher for the number
of links than for species richness. On the other hand, within-ecoregion
variability showed different bivariate relationships and a less constant
latitudinal gradient ([@Fig:ecoregion_bivariates]B). This indicates that
richness and links do not co-vary completely (i.e. their variability is not
closely connected) although they may show similar distributions for median
values.

![Bivariate relationship between community and network measures for the median
ecoregion value (A) and the within-ecoregion 89% interquantile range (B). Values
are grouped into three quantiles separately for each variable. The colour
combinations represent the nine possible combinations of quantiles. Species
richness (horizontal axis) goes left to right from low (light grey, bottom left)
to high (green, bottom right). The number of links goes bottom-up from low
(light grey, bottom left) to high (blue, top
left).](figures/ecoregion_bivariates.png){#fig:ecoregion_bivariates}

Our results also indicate a mismatch between the uniqueness of communities and
networks ([@Fig:ecoregion_lcbd]). Uniqueness was higher mostly in the north and
along the south border for communities, but only in the north for networks
([@Fig:ecoregion_lcbd]A-B). Consequently, ecoregions with both unique community
composition and unique network composition were mostly in the north
([@Fig:ecoregion_lcbd]C). Meanwhile, some areas were unique for one element but
not the other. For instance, the New England-Acadian forests ecoregion
(south-east, near 70°W and 48°N) had a highly unique species composition but a
more common network composition ([@Fig:ecoregion_lcbd]C). Opposite areas with
unique network compositions only were observed at higher between latitudes 52°N
and 70°N (Eastern Canadian Shield Taiga, Northern Canadian Shield Taiga,
Canadian Low Artic Tundra). Also, network uniqueness values for ecoregions
spanned a narrower range between the 44 ecoregions than species LCBD values
([@Fig:ecoregion_lcbd]D, left). Within-ecoregion variation was also lower for
network values with generally lower 89% interquantile ranges among the
site-level LCBD values ([@Fig:ecoregion_lcbd]D, right). Moreover, mismatched
sites (unique for only one element) formed two distinct groups when evaluating
the relationship between species richness and the number of links (see
Supplementary Material). The areas only unique for their species composition had
both a high richness and number of links. On the other hand, the sites only
unique for their networks had both lower richness and a lower number of links,
although they were not the sites with the lowest values for both.

![(A-B) Representation of the ecoregion uniqueness values based on species
composition (a) and network composition (b). LCBD values were first computed
across all sites and scaled relative to the maximum value observed. The
ecoregion LCBD value is the median value for the sites in the ecoregion. (C)
Bivariate representation of species and network composition LCBD. Values are
grouped into three quantiles separately for each variable. The colour
combinations represent the nine possible combinations of quantiles. The species
uniqueness (horizontal axis) goes left to right from low uniqueness (light grey,
bottom left) to high uniqueness (green, bottom right). The network composition
uniqueness goes bottom-up from low uniqueness (light grey, bottom left) to high
uniqueness (blue, top left). (D) Probability densities for the ecoregion LCBD
values for species and network LCBD (left), highlighting the variability of the
LCBD between ecoregions, and the 89% interquartile range of the values within
each ecoregion (right), highlighting the variability within the
ecoregions.](figures/ecoregion_LCBD_4panels.png){#fig:ecoregion_lcbd}

# Discussion

The spatial probabilistic metaweb we produced here is a first attempt at
downscaling a metaweb and producing localized predictions, as called for by
@Strydom2022PreMet. It gives us an idea of what local metawebs or networks could
look like in space, given the species distributions and their variability, as
well as the uncertainty around the interactions. We also provide the first
spatial representation of the metaweb of Canadian mammals [@Strydom2022FooWeb].
Conceptually, this is similar to how the European tetrapod metaweb
[@Maiorano2020TetSpe] was used to predict localized networks in Europe
[@Braga2019SpaAna; @OConnor2020UnvFoo; @Galiana2021SpaSca; @Gauzere2022DivBio;
@Botella2023LanInt]. Therefore, our approach could open similar possibilities of
investigations in North America with food webs of Canadian mammals, for instance
on the structure of food webs over space [@Braga2019SpaAna], on the scaling of
network area relationships [@Galiana2021SpaSca], and on the effect of land-use
intensification on food webs [@Botella2023LanInt]. Moreover, since our approach
is probabilistic, it does not assume species interact whenever they co-occur,
and incorporates variability based on environmental conditions, which could lead
to different results by introducing a different association between species
richness and network properties. @Galiana2021SpaSca found that species richness
had a large explanatory power over network properties but mentioned it could
potentially be due to interactions between species being fixed in space. Here,
we found mismatches in the distribution of species richness and interactions,
and especially regarding their within-ecoregion variability
([@Fig:ecoregion_bivariates]), highlighting that interactions might vary
differently than species distributions in space. Network measures (links on
[@Fig:ecoregion_bivariates]A) were also lower in the north, contrarily to
previous studies [e.g. connectance higher in the north, @Braga2019SpaAna;
@Galiana2021SpaSca].

Our LCBD and uniqueness results highlighted that areas with unique network
composition might differ from sites with unique species composition. In other
words, the joint distribution of community and network uniqueness highlights
different diversity hotspots. @Poisot2017HosPar showed a similar result with
host-parasite communities of rodents and ecto-fleas. Our results further show
how these differences could be distributed across ecoregions and a broad spatial
extent. Areas unique for only one element (species or network composition)
differed in their combination of species richness and number of links
(supplementary material), with species-unique sites displaying high values of
both measures and network-unique sites displaying low values. Moreover, LCBD
scores essentially highlight variability hotspots and are a measure of the
variance of community or network structure. Here they also serve as an
inter-ecoregion variation measure which can be compared to the within-ecoregion
variation highlighted by the interquantile ranges. The narrower range of values
for network LCBD values and the lower IQR values indicate that both the
inter-ecoregion and within-ecoregion variation are lower for network than for
species ([@Fig:ecoregion_lcbd]). Additionally, higher values for network LCBD
also indicate that most ecoregions can hold ecologically unique sites.

\newpage

# References
