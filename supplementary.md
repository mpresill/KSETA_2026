# Supplementary Material

# Madgraph basics: EFT event generation
**Setup**
We can download a local version of madgrpah from the official launchpage website 
```
wget https://launchpad.net/mg5amcnlo/3.0/3.6.x/+download/MG5_aMC_v3.7.0.tar.gz
```
then untar it and it's ready to go.

Before running, inspect the content of the folder, there is `model` folder, where you can copy the dedicated theory model decoding the feynman rules and particles you want to use - a very nice model database could be accessed at this feynrules page: https://feynrules.irmp.ucl.ac.be/wiki/ModelDatabaseMainPage (moment of glory: one of them is authored by me and student of my previous group, Sahar Ajmal).

Now, you can either prepare a text file with all commands in batch, or just run in the prompt. 
Either ways, you have to call `./bin/mg5_aMC (file_name.txt if you want to use batch mode)`

Out of the box MadGraph (MG) has no knowledge of EFT
MG allows for custom models to be imported
We’ll use ```SMEFTsim_topU3l_MwScheme``` (from SMEFTsim3.0 https://github.com/SMEFTsim/SMEFTsim/releases/tag/v3.0.2 )

---
**MG Syntax**
To generate a processes, simply use generate
Example:
```
generate pp > t t~
```
will generate events with a tt pair resulting from proton-proton collisions

**MG Syntax – decays**
We can build upon this using additional options such as specifying decays
```generate pp > t t~, (t > b l+ vl), (t~ > b~ j j)```
will ensure the top quark decays leptonically and the anti-top decays hadronically
The “,” syntax allows you to specify the decays, and the parathesis are syntactic sugar


**MG Syntax – more than one process**
The add process command will allows you to add more processes
```
generate pp > t t~, (t > b l+ vl), (t~ > b~ j j)
add process pp > t t~, (t > b j j), (t~ > b~ l- vl~)
```

will cover both possible decay modes for the semi-leptonic decay of the top quark
Another option is
```
generate pp > t t~ > b l+ vl b~ j j
add process pp > t t~ > b j j b~ l- vl~
```

The main difference is this command will include off-shell top quarks

**A few words on decays**
Having MG decay particles has its advantages, mainly
```
generate pp > t t~, (t > b l+ vl), (t~ > b~ l- vl~)
```
will pass the full spin correlation between the top quarks to the final-state leptons
However, specifying the decays in MG will significantly slow down the generation time
The other options are:
**MadSpin** – good for standard analyses like spin correlation; known to have issues with EFT
reweighting, so this is not recommended for EFT analyses
**Pythia** – Simply specify ```generate pp > t t~``` and let Pythia handle the decay of the
tops

---
**How to remove particles**
If we wanted to produce ttZ-like processes, we could use
```generate p p > t t~ l+ l-```
However, this will include all possible ways to produce two leptons,
including H → W+W−→ ℓ+ℓ− etc.
To exclude the Higgs boson from this process we can use
```generate p p > t t~ l+ l- / h```

---
**Including EFT effects**
Once you have a model installed (or specified in an extramodels card) you can import it
using
**import model SMEFTsim_topU3l_MwScheme_UFO**
This will instruct MG to load the SMEFTsim top U3l model, which will add EFT diagrams
e.g. ```pp > t t~``` will include both SM production (gluon-gluon fusion, qq annihilation) and
EFT vertices involving top quarks, gluons, and light quarks

**Extra partons**
Not possible for single-t processes
When possible, it is recommended to include one additional parton/final-state jet
For a tt process this would be
```
generate pp > t t~
add process pp > t t~ j
```
The extra jet brings our leading-order (LO) EFT simulations closer to
next-to-leading order (NLO)
A value for xqcut is also needed, which essentially tells MG what part of the phase space it should fill in for the extra jet

**EFT options**
* The SMEFTsim model has a few options to allow you to specify what EFT effects you want
* ```NP``` tells MG to enable “new physics”
* ```NP=1``` would allow for single insertion (one EFT vertex per diagram). This is the standard setting for EFT production.
* ```NP=2``` would allow double insertions, which is useful for probing both production and decay
* ```NPprop``` controls whether new physics can appear in propagators. We typically use ```NPprop=0```
* SMHLOOP controls Higgs-mediated loops: for LO samples we use ```SMHLOOP=0```
* Full example:
![](https://codimd.web.cern.ch/uploads/upload_adf9a6d7b7bd3e5876551320d87f7d7b.png)

---
**MG reweighting**
We typically us the reweighting procedure in MG instead of generating several gridpacks for dedicated EFT points.
A reweight card is included to tell MG what values we want:![](https://codimd.web.cern.ch/uploads/upload_fdf08f0a58c6c26070220267732e1e5b.png)

The templates needed can be generated in two complementary ways either by *amplitude decomposition* or with *reweighting*. 

With amplitude decomposition the single components (SM, Lin $\_{\alpha}$, Quad $\_{\alpha}$, Mix $\_{\alpha, \beta}$) can be generated. For example exploiting [MadGraph](http://madgraph.phys.ucl.ac.be/) and [SMEFTsim](https://smeftsim.github.io/) one can do as follows:


---
# A few examples

**SM**:
```
import model SMEFTsim_U35_MwScheme_UFO-SMlimit_massless
generate p p > e+ ve mu- vm~
output WW_SM
```

**Lin**:
```
import model SMEFTsim_U35_MwScheme_UFO-cW_massless
generate p p > e+ ve mu- vm~ NP=1 NP^2==1
output WW_LI
```

**Quad**:
```
import model SMEFTsim_U35_MwScheme_UFO-cW_massless
generate p p > e+ ve mu- vm~ NP=1 NP^2==2
output WW_QU
```

**Mix**:
```
import model SMEFTsim_U35_MwScheme_UFO-cW_cHW_massless
generate p p > e+ ve mu- vm~ NP=1 NP^2==1
output WW_Mix
```

With the reweighting method one can generatefrom the full Lagrangian + one operator and extract the components thanks to a reweighting procedure.
Suppose we start our generation by including all terms, setting the coupling of $c\_{W}=1$

**SM+Lin+Quad**:
```
import model SMEFTsim_U35_MwScheme_UFO-cW_massless
generate p p > e+ ve mu- vm~ NP=1
output WW_Reweight
```

We can now change at reweighting the coupling in order to generate different components

**SM**:

```
change helicity False
change rwgt_dir rwgt

# SM: rwgt_1
launch
   set SMEFT 2 0
```
**SM-Lin+Quad**:

```
# SM - Lin + Quad: rwgt_2
launch
   set SMEFT 2 -1
```

Each event will now have two new reweighting - weights corresponding to the hypothesis $c\_W = 0$ ( $\omega(k=0)$ ) and $c\_W = -1$ ( $\omega(k=-1)$ ). The nominal weight corresponds to the hypothesis $c\_W = 1$ ( $\omega(k=1)$ ). 
Event by event we can add these weights to obtain the Sm / Quadratic / Linear components:

$$ 
\begin{equation}
\begin{cases}
\omega\_{\text{Quad}} = 0.5 \cdot \left [ \omega(k=1) + \omega(k=-1) - 2 \cdot \omega(k=0) \right ] \\
\omega\_{\text{SM}} = \omega(k=0)\\
\omega\_{\text{Lin}} = 0.5 \cdot \left [ \omega(k=1) - \omega(k=-1) \right ]\\
\end{cases}
\end{equation}
$$

For more operators one can generate the components for a single operator by setting all the others at 0 and scanning the values -1,0,1 as described above. For the mixed term instead one should also generate the weight:

```
# SM + Lin + Quad + Lin + Quad + Mix: rwgt_3
launch
   set SMEFT 2 1
   set SMEFT 7 1
```

And the algebra on the weights reads as follows 

$$ 
\omega\_{\text{Mix}} = \omega(1,1) + \omega(0,0) - \omega(1,0) - \omega(0,1)
$$

We stress that these weights should be computed on an event-by-event basis.


---
# Rivet basics
* https://indico.cern.ch/event/1578743/contributions/6710604/attachments/3140870/5578042/CMS_Rivet_tutorial.pdf 

---
# Roofit basics

* Please refer to this tutorial: https://cms-analysis.github.io/HiggsAnalysis-CombinedLimit/latest/part5/roofit/ 
* and this turorial: https://github.com/amarini/Prefit2020 (introduced here: https://indico.cern.ch/event/817757/contributions/3712523/attachments/2000027/3338337/Presentation_Session1.pdf)

---
## Extra

- more on nanoGEN: https://indico.fnal.gov/event/68174/contributions/316669/attachments/189121/261176/LPC_EFT_GEN_2025.pdf 
