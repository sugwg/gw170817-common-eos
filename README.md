# Constraining the nuclear equation of state with GW170817

**Soumi De<sup>1</sup>, Daniel Finstad<sup>1</sup>, James M. Lattimer<sup>2</sup>, Duncan A. Brown<sup>1</sup>, Edo Berger<sup>3</sup>, Christopher M. Biwer<sup>1,4</sup>**

**<sup>1</sup>Department of Physics, Syracuse University, Syracuse, NY 13244, USA**

**<sup>2</sup>Department of Physics and Astronomy, Stony Brook University, Stony Brook, NY 11794-3800, USA**

**<sup>3</sup>Harvard-Smithsonian Center for Astrophysics, Cambridge, Massachusetts 02139, USA**

**<sup>4</sup>Applied Computer Science (CCS-7), Los Alamos National Laboratory, Los Alamos, NM, 87545, USA**

## License

![Creative Commons License](https://i.creativecommons.org/l/by-sa/3.0/us/88x31.png "Creative Commons License")

This work is licensed under a [Creative Commons Attribution-ShareAlike 3.0 United States License](http://creativecommons.org/licenses/by-sa/3.0/us/).

## Introduction

This notebook is a companion to the paper posted at [arxiv:1804.08583v2](https://arxiv.org/abs/1804.08583v2). It demonstrates how to read and use our posterior probability density files from the MCMC and shows how to reconstruct figures 2 and 3 in the main text and figures 4 and 6 in the supplementary material from the raw data.

We encourage use of these data in derivative works. If you use the material provided here, please cite the paper using the reference:
```
@article{De:2018uhw,
      author         = "De, Soumi and Finstad, Daniel and Lattimer, James M. and
                        Brown, Duncan A. and Berger, Edo and Biwer, Christopher
                        M.",
      title          = "{Constraining the nuclear equation of state with
                        GW170817}",
      year           = "2018",
      eprint         = "1804.08583",
      archivePrefix  = "arXiv",
      primaryClass   = "astro-ph.HE",
      SLACcitation   = "%%CITATION = ARXIV:1804.08583;%%"
}
```

The data provided contain the thinned posterior samples from the MCMC chains used to produce the posterior probability density plots and the Bayes factors. These data are stored in the files:

 1. [dns_mass_prior_common_eos_20hz_lowfreq_posteriors.hdf](https://github.com/sugwg/gw170817-common-eos/blob/master/dns_mass_prior_common_eos_20hz_lowfreq_posteriors.hdf) contains a thinned chain of the posterior samples from the MCMC where we use the common EOS constraint, 0 < Lambda_s < 5000, the double neutron star mass prior, and a 20 Hz low-frequency cutoff in the analysis.
 2. [dns_mass_prior_common_eos_20hz_lowfreq_posteriors_long_chain.hdf](https://github.com/sugwg/gw170817-common-eos/blob/master/dns_mass_prior_common_eos_20hz_lowfreq_posteriors_long_chain.hdf) contains a thinned chain of the posterior samples from the MCMC where we use the common EOS constraint, 0 < Lambda_s < 5000, the double neutron star mass prior, and a 20 Hz low-frequency cutoff in the analysis. -- used for Bayes factor calculation in the paper. This is a larger file with more samples than the file above.
 3. [dns_mass_prior_independent_lambdas_20hz_lowfreq_posteriors_long_chain.hdf](https://github.com/sugwg/gw170817-common-eos/blob/master/dns_mass_prior_independent_lambdas_20hz_lowfreq_posteriors_long_chain.hdf) contains a thinned chain of the posterior samples from the MCMC where the individual star's tidal deformation parameters are uncorrelated, 0 < Lambda_1 < 1000, 0 < Lambda_2 < 5000, use the double neutron star mass prior, and a 20 Hz low-frequency cutoff in the analysis -- used for Bayes factor calculation in the paper.
 4. [galactic_ns_mass_prior_common_eos_20hz_lowfreq_posteriors.hdf](https://github.com/sugwg/gw170817-common-eos/blob/master/galactic_ns_mass_prior_common_eos_20hz_lowfreq_posteriors.hdf) contains a thinned chain of the posterior samples from the MCMC where we use the common EOS constraint, 0 < Lambda_s < 5000, the Galactic neutron star mass prior, and a 20 Hz low-frequency cutoff in the analysis.
 5. [galactic_ns_mass_prior_common_eos_20hz_lowfreq_posteriors_long_chain.hdf](https://github.com/sugwg/gw170817-common-eos/blob/master/galactic_ns_mass_prior_common_eos_20hz_lowfreq_posteriors_long_chain.hdf) contains a thinned chain of the posterior samples from the MCMC where we use the common EOS constraint, 0 < Lambda_s < 5000, the Galactic neutron star mass prior, and a 20 Hz low-frequency cutoff in the analysis -- used for Bayes factor calculation in the paper. This is a larger file with more samples than the file above.
 6. [galactic_ns_mass_prior_independent_lambdas_20hz_lowfreq_posteriors_long_chain.hdf](https://github.com/sugwg/gw170817-common-eos/blob/master/galactic_ns_mass_prior_independent_lambdas_20hz_lowfreq_posteriors_long_chain.hdf) contains a thinned chain of the posterior samples from the MCMC where the individual star's tidal deformation parameters are uncorrelated, 0 < Lambda_1 < 1000, 0 < Lambda_2 < 5000, use the Galactic neutron star mass prior, and a 20 Hz low-frequency cutoff in the analysis -- used for Bayes factor calculation in the paper.
 7. [uniform_mass_prior_common_eos_20hz_lowfreq_posteriors.hdf](https://github.com/sugwg/gw170817-common-eos/blob/master/uniform_mass_prior_common_eos_20hz_lowfreq_posteriors.hdf) contains a thinned chain of the posterior samples from the MCMC where we use the common EOS constraint, 0 < Lambda_s < 5000, the uniform mass prior, and a 20 Hz low-frequency cutoff in the analysis.
 8. [uniform_mass_prior_common_eos_20hz_lowfreq_posteriors_long_chain.hdf](https://github.com/sugwg/gw170817-common-eos/blob/master/uniform_mass_prior_common_eos_20hz_lowfreq_posteriors_long_chain.hdf) contains a thinned chain of the posterior samples from the MCMC where we use the common EOS constraint, 0 < Lambda_s < 5000, the uniform mass prior, and a 20 Hz low-frequency cutoff in the analysis -- used for Bayes factor calculation in the paper. This is a larger file with more samples than the file above.
 9. [uniform_mass_prior_independent_lambdas_20hz_lowfreq_posteriors_long_chain.hdf](https://github.com/sugwg/gw170817-common-eos/blob/master/uniform_mass_prior_independent_lambdas_20hz_lowfreq_posteriors_long_chain.hdf) contains a thinned chain of the posterior samples from the MCMC where the individual star's tidal deformation parameters are uncorrelated, 0 < Lambda_1 < 1000, 0 < Lambda_2 < 5000, use the uniform mass prior, and a 20 Hz low-frequency cutoff in the analysis -- used for Bayes factor calculation in the paper.
 10. [uniform_mass_prior_lambda_s_lessthan100_20hz_lowfreq_posteriors_long_chain.hdf](https://github.com/sugwg/gw170817-common-eos/blob/master/uniform_mass_prior_lambda_s_lessthan100_20hz_lowfreq_posteriors_long_chain.hdf) contains a thinned chain of the posterior samples from the MCMC where we use the common EOS constraint, the uniform mass prior, require 0 < Lambda_s < 100, and a 20 Hz low-frequency cutoff in the analysis -- used for Bayes factor calculation in the paper.
 11. [uniform_mass_prior_common_eos_25hz_lowfreq_posteriors.hdf](https://github.com/sugwg/gw170817-common-eos/blob/master/uniform_mass_prior_common_eos_25hz_lowfreq_posteriors.hdf) contains a thinned chain of the posterior samples from the MCMC where we use the common EOS constraint, 0 < Lambda_s < 5000, the uniform mass prior, and a 25 Hz low-frequency cutoff in the analysis.
 12. [independent_lambda_uniform_mass_30hz_lowfreq_posterior.hdf](https://github.com/sugwg/gw170817-common-eos/blob/master/independent_lambda_uniform_mass_30hz_lowfreq_posterior.hdf) contains the posterior samples from the MCMC where we do not apply the common EOS constraint allowing the tidal deformability parameters of the component stars Lambda_1,2 to vary independently between 0 and 3000, use the uniform [1.0, 2.0] M_sun mass prior, and a 30 Hz low-frequency cutoff in the analysis. This is used to compare our results to Fig. 5 of [Abbott et al. (2017)](https://journals.aps.org/prl/abstract/10.1103/PhysRevLett.119.161101).

The results used in the paper were generated with the [PyCBC v1.9.4 release.](https://github.com/gwastro/pycbc/releases/tag/v1.9.4)

## Running this notebook in a Docker container

This notebook can be run from a PyCBC Docker container, or a machine with PyCBC installed. Instructions for [downloading the docker container](http://gwastro.github.io/pycbc/latest/html/docker.html) are available from the [PyCBC home page.](https://pycbc.org/) To start a container with instance of Jupyter notebook, run the commands
```sh
docker pull pycbc/pycbc-el7:v1.9.4
docker run -p 8888:8888 --name pycbc_notebook -it pycbc/pycbc-el7:v1.9.4 /bin/bash -l
```
Once the container has started, this git repository can be downloaded with the command:
```sh
git clone https://github.com/sugwg/gw170817-common-eos.git
```
The notebook server can be started inside the container with the command:
```sh
jupyter notebook --ip 0.0.0.0 --no-browser
```
You can then connect to the notebook server at the URL printed by ``jupyter``. Navigate to the directory `gw170817-common-eos` in the cloned git repository and open [data_release_common_eos_companion.ipynb](https://github.com/sugwg/gw170817-common-eos/blob/master/data_release_common_eos_companion.ipynb) (this notebook).

## Acknowledgements

We thank Stefan Ballmer, Swetha Bhagwat, Steven Reyes, Andrew Steiner, and Douglas Swesty for helpful discussions. We particularly thank Collin Capano and Alexander Nitz for contributing to the development of PyCBC Inference; however, they did not wish to be authors due to restrictions placed by LIGO Scientific Collaboration policies.


## Funding

This work was supported by NSF awards PHY-1404395 (DAB, CMB), PHY-1707954 (DAB, SD, DF), AST-1714498 (EB), and DOE Award DE-FG02-87ER40317 (JML). Computations were supported by Syracuse University and NSF award OAC-1541396. DAB, EB, SD, and JML thank Kavli Institute for Theoretical Physics which is supported by the NSF award PHY-1748958.
